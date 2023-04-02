---
sidebar_position: 1
sidebar_label: Manage A Liquidity Position
---

# Manage A Liquidity Position

## Introduction

Like Joe V1, managing liquidity on Joe V2.1 can be executed through a router contract called `LBRouter`. This contract will abstract some of the complexity of the liquidity management, perform safety checks and will revert if certain conditions were to not be met. This is recommended way to use Joe V2.1 for most users.

In contrast to V1, liquidity can be concentrated in arbitrary shapes and any price range the user desires.

Next sections explain how to:

- How are new pairs created
- How to add liquidity
- How to remove liquidity

## Pair Creation

To create a new pair, the `createLBPair` function of the `LBFactory` contract is called.

```js
function createLBPair(
    IERC20 tokenX,
    IERC20 tokenY,
    uint24 activeId,
    uint16 binStep
) external returns (ILBPair pair);
```

The pair creator sets the initial price via the `activeId` argument.

It is important to note that there can be multiple markets of the same pair, but only differing in their bin step.

Pools are therefore uniquely identified by the tuple `(tokenX, tokenY, binStep)`.

After pair creation tokens can be added to any desired bin provided that:

- Above bin `activeId` only `tokenX` can be added
- Below bin `activeId` only `tokenY` can be added
- Both `tokenX` and `tokenY` liquidity can be added to bin `activeId`

## Adding Liquidity

To add liquidity, the `LiquidityParameters` struct is as input:

```js
function addLiquidity(LiquidityParameters memory liquidityParameters)
    external
    returns (
        uint256 amountXAdded,
        uint256 amountYAdded,
        uint256 amountXLeft,
        uint256 amountYLeft,
        uint256[] memory depositIds,
        uint256[] memory liquidityMinted
    );

function addLiquidityNATIVE(LiquidityParameters memory liquidityParameters)
    external
    payable
    returns (
        uint256 amountXAdded,
        uint256 amountYAdded,
        uint256 amountXLeft,
        uint256 amountYLeft,
        uint256[] memory depositIds,
        uint256[] memory liquidityMinted
    );
```

### Liquidity Parameters

```js
struct LiquidityParameters {
    IERC20 tokenX; // Has to be the same as tokenX defined in LBPair contract
    IERC20 tokenY; // Has to be the same as tokenY defined in LBPair contract
    uint256 binStep; // Has to point to existing pair
    uint256 amountX; // Amount of token X that you want to add to liquidity
    uint256 amountY; // Amount of token Y that you want to add to liquidity
    uint256 amountXMin; // Defines amount slippage for token X
    uint256 amountYMin; // Defines amount slippage for token Y
    uint256 activeIdDesired; // The active bin you want. It may change due to slippage
    uint256 idSlippage; // The slippage tolerance in case active bin moves during time it takes to transact
    int256[] deltaIds; // The bins you want to add liquidity to. Each value is relative to the active bin ID
    uint256[] distributionX; // The percentage of X you want to add to each bin in deltaIds
    uint256[] distributionY; // The percentage of Y you want to add to each bin in deltaIds
    address to; // Receiver address
    address refundTo; // Refund Address
    uint256 deadline; // Block timestamp cannot be lower than deadline
}
```

The number of parameters are quite extensive. Here are a few pointers to understand how to construct them better:

- The active bin ID may change from the time you decided to add liquidity to when it is actually added. Therefore, you define `activeIdDesired` and `idSlippage` to account for when the price moves.
- `deltaIds` define which bins liquidity will be added to relative to `activeId`, 0 being the active bin. All positive values are bins with only X and all negative values are bins with only Y.
- `distributionX` (or `distributionY`) is the percentages of `amountX` (or `amountY`) you want to add to each bin.
  - Sum of all values should be less than or equal to 1. If less than, the remaining is refunded back to the user.
  - Trying to add X to a bin below the active bin or Y to a bin above the active bin will cause a revert.
- Maximum number of bins, that can be populated at the same time is around `80` on Avalanche C-chain due to block gas limit (`8M`). Multiple transactions can be used to add liquidity to more bins.

### Code Example

In this example, we add 100 USDC and 100 USDT into three bins: active bin, bin below and bin above.

We define the distributions as follow:

- For asset X (USDC), we add 50 USDC to the active bin and 50 USDC to the bin above.
- For asset Y (USDT), we add 33.3 USDT to the active bin and 66.6 USDT to the bin below.

We also allow a bin ID slippage of 5 just in case bin moves in the time it takes to execute the transaction.

```js
uint256 PRECISION = 1e18;
uint256 binStep = 25;
uint256 amountX = 100 * 10e6;
uint256 amountY = 100 * 10e6;
uint256 amountXmin = 99 * 10e6; // We allow 1% amount slippage
uint256 amountYmin = 99 * 10e6; // We allow 1% amount slippage

uint256 activeIdDesired = 2**23; // We get the ID from price using getIdFromPrice()
uint256 idSlippage = 5;

uint256 binsAmount = 3;
int256[] memory deltaIds = new int256[](binsAmount);
deltaIds[0] = -1;
deltaIds[1] = 0;
deltaIds[2] = 1;
uint256[] memory distributionX = new uint256[](binsAmount);
distributionX[0] = 0;
distributionX[1] = PRECISION / 2;
distributionX[2] = PRECISION / 2;

uint256[] memory distributionY = new uint256[](binsAmount);
distributionY[0] = (2 * PRECISION) / 3;
distributionY[1] = PRECISION / 3;
distributionY[2] = 0;


ILBRouter.LiquidityParameters memory liquidityParameters = ILBRouter.LiquidityParameters(
    USDC,
    USDT,
    binStep,
    amountX,
    amountY,
    amountXmin,
    amountYmin,
    activeIdDesired,
    idSlippage,
    deltaIds,
    distributionX,
    distributionY,
    receiverAddress,
    refundAddress,
    block.timestamp
);

USDC.approve(address(router), amountX);
USDT.approve(address(router), amountY);

(
    uint256 amountXAdded,
    uint256 amountYAdded,
    uint256 amountXLeft,
    uint256 amountYLeft,
    uint256[] memory depositIds,
    uint256[] memory liquidityMinted
) = router.addLiquidity(liquidityParameters);
```

## Removing Liquidity

There are some key differences between adding and removing liquidity:

1. We don't use the `LiquidityParameters` struct.
2. We use absolute bin IDs instead of relative bin IDs.
3. Because we use absolute bin IDs, bin slippage is not possible.
4. We define absolute `LBToken` balances to remove from each bin.
   - In bins below active bin, balances consist of only Y.
   - In bins above active bin, balances consist of only X.
   - In the active bin, the balance consists of a share of X and Y.

To remove liquidity, we use one of the router functions below:

```js
function removeLiquidity(
    IERC20 tokenX,
    IERC20 tokenY,
    uint16 binStep, // Has to point to existing pair that user has liquidity deposited in
    uint256 amountXMin, // Minimum amount of token X that has to be withdrawn
    uint256 amountYMin, // Minimum amount of token Y that has to be withdrawn
    uint256[] memory ids, // Bin IDs that liquidity should be removed from
    uint256[] memory amounts, // LBToken amount that should be removed
    address to, // Receiver address
    uint256 deadline // Block timestamp cannot be lower than deadline
) external returns (uint256 amountX, uint256 amountY);

function removeLiquidityNATIVE(
    IERC20 token,
    uint16 binStep,
    uint256 amountTokenMin,
    uint256 amountNATIVEMin,
    uint256[] memory ids,
    uint256[] memory amounts,
    address payable to,
    uint256 deadline
) external returns (uint256 amountToken, uint256 amountNATIVE);
```

Here are some pointer for using these functions:

1. Lengths of `ids` and `amounts` must be the same.
2. Values in `amounts` are `LBToken` amounts.
3. Maximum number of bins that can be withdrawn at the same time is around `51` due to Avalanche C-chain block gas limit (`8M`). In this case, multiple transactions can be used to remove more liquidity.

### Code Example

```js
uint256 numberOfBinsToWithdraw = 3;
uint16 binStep = 25;

uint256[] memory amounts = new uint256[](numberOfBinsToWithdraw);
uint256[] memory ids = new uint256[](numberOfBinsToWithdraw);
ids[0] = 8388608;
ids[1] = 8388611;
ids[2] = 8388605;
uint256 totalXBalanceWithdrawn;
uint256 totalYBalanceWithdrawn;

// To figure out amountXMin and amountYMin, we calculate how much X and Y underlying we have as liquidity
for (uint256 i; i < numberOfBinsToWithdraw; i++) {
    uint256 LBTokenAmount = pair.balanceOf(receiverAddress, ids[i]);
    amounts[i] = LBTokenAmount;
    (uint256 binReserveX, uint256 binReserveY) = pair.getBin(uint24(ids[i]));

    totalXBalanceWithdrawn += LBTokenAmount * binReserveX / pair.totalSupply(ids[i]);
    totalYBalanceWithdrawn += LBTokenAmount * binReserveY / pair.totalSupply(ids[i]);
}

uint256 amountXMin = totalXBalanceWithdrawn * 99 / 100; // Allow 1% slippage
uint256 amountYMin = totalYBalanceWithdrawn * 99 / 100; // Allow 1% slippage

pair.approveForAll(address(router), true);

router.removeLiquidity(
    USDC,
    WAVAX,
    binStep,
    amountXMin,
    amountYMin,
    ids,
    amounts,
    receiverAddress,
    block.timestamp
);
```
