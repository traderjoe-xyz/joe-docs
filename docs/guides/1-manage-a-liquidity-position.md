---
sidebar_position: 1
sidebar_label: Manage A Liquidity Position
---

# Manage A Liquidity Position

## Introduction

Like Joe v1, managing liquidity on Joe v2 can be executed through a router contract called `LBRouter`. This contract will abstract some of the complexity of the liquidity management, perform safety checks and will revert if certain conditions were to not be met. This is recommended way to use Joe v2 for most users.

In contrast to v1, liquidity can be concentrated in arbitrary shapes and never covers price range from 0 to infinity. It is crucial to properly understand and define required bin distributions before starting liquidity management. Basic concepts are explained under [Concentrated Liquidity](../concepts/0-concentrated-liquidity.md) and [Bin Liquidity](../concepts/1-bin-liquidity.md). You can find more technical approach below.

Next paragraphs will explain how to manage a liquidity position, namely:
- How are new pairs created.
- How to add liquidity:
    - Which functions to use.
    - How to properly select liquidity parameters.
    - How to use them in code example.
    - How to choose bin distributions based on chosen goals.
- How to remove liquidity:
    - Which functions to use.
    - How to properly select arguments.
    - How to use them in code example.

## Pair creation

Creating new pools is not permissionless at the moment of launch - `creationUnlocked()` function of `LBFactory` returns `false`.

During pair creation `createLBPair` function of `LBFactory` contract is called. 

```js
function createLBPair(
    IERC20 tokenX,
    IERC20 tokenY,
    uint24 activeId,
    uint16 binStep
) external returns (ILBPair pair);
```

`activeId` argument sets initial price.

After pair creation tokens can be added to any desired bin provided that: 
- Above bin `activeId` only `tokenX` liquidity can be added
- Below bin `activeId` only `tokenY` liquidity can be added
- Both `tokenX` and `tokenY` liquidity can be added to bin `activeId`

## Adding liquidity with LBRouter

To add liquidity using struct `LiquidityParameters` defined in contract `ILBRouter` should be used as an input to function:

```js
function addLiquidity(LiquidityParameters memory liquidityParameters)
    external
    returns (uint256[] memory depositIds, uint256[] memory liquidityMinted);

function addLiquidityAVAX(LiquidityParameters memory liquidityParameters)
    external
    payable
    returns (uint256[] memory depositIds, uint256[] memory liquidityMinted);

```

### Liquidity parameters

```js
struct LiquidityParameters {
    IERC20 tokenX; // Has to be the same as tokenX defined in LBPair contract
    IERC20 tokenY; // Has to be the same as tokenY defined in LBPair contract
    // Will revert if wrong order given
    uint256 binStep; // Has to point to existing pair
    uint256 amountX; // Amount of token X that you want to add to liquidity
    uint256 amountY; // Amount of token Y that you want to add to liquidity
    uint256 amountXMin; // Defines amount slippage for token X
    uint256 amountYMin; // Defines amount slippage for token X
    // In practice amount slippage defined by amountXMin/amountYMin will never be significant if distributions are set properly
    uint256 activeIdDesired; // Currently active bin
    uint256 idSlippage; // If price (active bin) moves more than that, transaction will revert
    int256[] deltaIds; // Delta between active bin and bin, which given distribution is added to
    uint256[] distributionX; // Defines part of amountX that should be added to bin (activeIdDesired[i] + deltaIds[i])
    uint256[] distributionY; // Defines part of amountY that should be added to bin (activeIdDesired[i] + deltaIds[i])

    address to; // Receiver address
    uint256 deadline; // Block timestamp cannot be lower than deadline
}
```


`deltaIds` define, which bins liquidity will be added to, relatively to `activeId`. `idSlippage` defines, how can `activeId` differ from `activeIdDesired` during transaction.

`distributionX`, `distributionY` define, how tokens (`amountX`, `amountY`) will be spread across chosen bins.

Take below points into account while choosing `LiquidityParameters` argument:
1. Sum of all values in `distributionX` array has to be less or equal to `Constants.PRECISION`.
2. Sum of all values in `distributionY` array has to be less or equal to `Constants.PRECISION`.
3. Distributions can take all shapes and values, and are set independently.
4. If sum of all `distributionX` (`distributionY`) values is not equal to `Constants.PRECISION`, full `amountX` (`amountY`) value will not be deposited. Plan `amountXmin` (`amountYmin`) accordingly.
5. Any excess funds (sent to router, but not added) will be sent back to the user.
6. `_distributionX` for `deltaIds < 0` (so `bin IDs < activeIdDesired`) has to be `0`.
7. `_distributionY` for `deltaIds > 0` (so `bin IDs > activeIdDesired`) has to be `0`.
8. For every bin in `deltaIds` array at least one of the distributions has to be more than `0`.
9. Lengths of distribution arrays and delta ID array have to be the same.
10. Maximum number of bins, that can be populated at the same time is around `51` due to Avalanche blockchain block gas limit (`8M`). Multiple transactions can be used to add liquidity to more bins.
11. If you want to add liquidity only to one token, use `amountX = 0` or `amountY = 0` and appropriate `_deltaIds`.
12. When adding liquidity to AVAX pair, `tokenX`/`tokenY` has to be WAVAX and `value` of transaction has to be equal to `amountX`/`amountY`.
13. Remember to approve spending `tokenX`/`tokenY` by `LBRouter`.

### Code sample

```js
uint256 PRECISION = 1e18;
uint256 binStep = 25; 
uint256 _amountX = 100 * 10e6; 
uint256 _amountY = 100 * 10e6;
uint256 _amountXmin = 99 * 10e6; //allow 1% amount slippage
uint256 _amountYmin = 99 * 10e6; //allow 1% amount slippage

uint256 _activeIdDesired = 2**23; 
uint256 _idSlippage = 5; 

uint256 _binsAmount = 3;
int256[] memory _deltaIds = new int256[](_binsAmount);
_deltaIds[0] = -1;
_deltaIds[1] = 0;
_deltaIds[2] = 1;
uint256[] memory _distributionX = new uint256[](_binsAmount);
_distributionX[0] = 0;
_distributionX[1] = PRECISION / 2;
_distributionX[2] = PRECISION / 2;

uint256[] memory _distributionY = new uint256[](_binsAmount);
_distributionY[0] = (2 * PRECISION) / 3;
_distributionY[1] = PRECISION / 3;
_distributionY[2] = 0;

address _receiverAddress = DEV;
uint256 _deadline = block.timestamp; //use safer value

ILBRouter.LiquidityParameters memory _liquidityParameters = ILBRouter.LiquidityParameters(
    USDC,
    USDT,
    binStep,
    _amountX,
    _amountY,
    _amountXmin,
    _amountYmin,
    _activeIdDesired,
    _idSlippage,
    _deltaIds,
    _distributionX,
    _distributionY,
    _receiverAddress,
    _deadline
);

// approve spending by router
USDC.approve(address(router), _amountX);
USDT.approve(address(router), _amountY);

(uint256[] memory depositIds, uint256[] memory liquidityMinted) = router.addLiquidity(_liquidityParameters);
```

### Distribution examples

1. Deposit only token X, above current price. If price moves in desired direction, tokenY + accrued fees can be withdrawn from every bin independently - DCA strategy.
```
_deltaIds = [1, 11, 33],  
_distributionX = [PRECISION / 3, PRECISION / 3, PRECISION / 3], 
_amountY & _amountYmin = 0
```

2. Deposit all tokens to a single bin - maximum capital concentration; no more fees will be accrued if active bin changes.
```
_deltaIds = [0], 
_distributionX = [PRECISION],
_distributionY = [PRECISION]
```

3. Deposit tokens to earn fees only during high volatility of stable pair. No fees earned while `priceX ~ priceY`, high fees accrued while price deviates.
```
_deltaIds = [-6, -5, 5, 6],  
_distributionX = [0, 0, PRECISION / 2, PRECISION / 2], 
_distributionY = [PRECISION / 2, PRECISION / 2, 0, 0]
```

## Removing liquidity with LBRouter

There are some key differences between adding and removing liquidity, when function parameters are considered, mainly:
1. No bin slippage possible - absolute bin values are chosen (not relative to active bin).
2. `tokenX`/`tokenY` order doesn't matter.
3. `LBtoken` balances to remove are stated explicitly (not relatively with `Constants.PRECISION` parameter) 

To remove liquidity using Router one of following functions should be used:

```js
function removeLiquidity(
    IERC20 tokenX,
    IERC20 tokenY,
    uint16 binStep, // Has to point to existing pair, that user has liquidity deposited in
    uint256 amountXMin, // Minimum amount of token X, that has to be withdrawn
    uint256 amountYMin, // Minimum amount of token Y, that has to be withdrawn
    uint256[] memory ids, // Bin IDs that liquidity should be removed from
    uint256[] memory amounts, // LBToken amount, that should be removed
    address to, // Receiver address
    uint256 deadline // Block timestamp cannot be lower than deadline
) external returns (uint256 amountX, uint256 amountY);

function removeLiquidityAVAX(
    IERC20 token,
    uint16 binStep,
    uint256 amountTokenMin,
    uint256 amountAVAXMin,
    uint256[] memory ids,
    uint256[] memory amounts,
    address payable to,
    uint256 deadline
) external returns (uint256 amountToken, uint256 amountAVAX);
```

Arrays `ids` and `amounts` define, which bin IDs will be withdrawn, and how many LBTokens will be withdrawn.

Take below points into account while choosing arguments for `removeLiquidity` functions:
1. `amountXMin` and `amountYMin` define amount slippage - if liquidity removal yields less tokens, it will revert with `LBRouter__AmountSlippageCaught`. Amount slippage might occur, when bin composition or active bin change due to swaps.
2. Lengths of `ids` and `amounts` must be the same.
3. `amounts` array consists of `LBToken` balances, not `tokenX`/`tokenY` balances; in case of active bin change it's possible that unexpected token is withdrawn.
4. `tokenX`/`tokenY` order doesn't matter.
5. Maximum number of bins, that can be withdrawn at the same time is around `51` due to Avalanche blockchain block gas limit (`8M`). In this case, multiple transactions can be used to remove more liquidity.

### Code example

Below code example includes no slippage or bin composition change - might revert, if computation done off-chain and/or during high market volatility.

Steps to withdraw liquidity:

1. Choose bin IDs, that are to be withdrawn (`uint256[] memory ids`).
2. Check `LBToken` balances owned. Any amount can be withdrawn, 100% withdrawn in below code example (`uint256[] memory amounts`).
3. Compute how many underlying assets should be withdrawn during current conditions and set accepted slippage.
4. Approve spending `LBToken` by `LBRouter`.
5. Remove liquidity

```js
uint256 _numberOfBinsToWithdraw = 3;

uint256[] memory amounts = new uint256[](_numberOfBinsToWithdraw);
uint256[] memory ids = new uint256[](_numberOfBinsToWithdraw);
ids[0] = 8388608;
ids[1] = 8388611;
ids[2] = 8388605;
uint256 totalXbalanceWithdrawn;
uint256 totalYBalanceWithdrawn;

for (uint256 i; i < _numberOfBinsToWithdraw; i++) {
    uint256 LBTokenAmount = pair.balanceOf(DEV, ids[i]);
    amounts[i] = LBTokenAmount;
    (uint256 binReserveX, uint256 binReserveY) = pair.getBin(uint24(ids[i]));

    bool hasXBalanceInBin = (LBTokenAmount != 0) && (binReserveX != 0);
    bool hasYBalanceInBin = (LBTokenAmount != 0) && (binReserveY != 0);
    totalXbalanceWithdrawn += hasXBalanceInBin ? (LBTokenAmount * binReserveX - 1) / pair.totalSupply(ids[i]) + 1 : 0;
    totalYBalanceWithdrawn += hasYBalanceInBin ? (LBTokenAmount * binReserveY - 1) / pair.totalSupply(ids[i]) + 1 : 0;
}

pair.setApprovalForAll(address(router), true);

router.removeLiquidity(
    token6D,
    token18D,
    binStep,
    totalXbalanceWithdrawn,
    totalYBalanceWithdrawn, 
    ids,
    amounts,
    DEV,
    block.timestamp
);
```