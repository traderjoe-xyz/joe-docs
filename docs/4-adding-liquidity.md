---
id: Adding Liquidity
---

To add liquidity using router struct `LiquidityParameters` from `ILBRouter.sol` should be used as an input to function

```
function addLiquidity(LiquidityParameters memory liquidityParameters)
        external
        returns (uint256[] memory depositIds, uint256[] memory liquidityMinted);
```

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

Distributions + delta IDs define, how tokens will be spread across bins.
Liquidity deposited is always dependent on bin, that is active during transaction. `idSlippage` defines, how much can actual distribution differ from `activeIdDesired`.

Take below points into account while choosing LiquidityParameters:
1. Sum of all values in `distributionX` array has to be less or equal to `Constants.PRECISION`
2. Sum of all values in `distributionY` array has to be less or equal to `Constants.PRECISION`
3. Distributions can take all shapes and values, and are set independently
4. If sum of all `distributionX` (`distributionY`) values for is not equal to `Constants.PRECISION`, full `amountX` (`amountY`) value will not be deposited. Plan `amountXmin` (`amountYmin`) accordingly
5. Any excess funds (sent to router, but not added) will be sent back to the user
6. `_distributionX` for `IDs < activeIdDesired`has to be `0`
7. `_distributionY` for `IDs > activeIdDesired` has to be `0`
8. For every bin in `deltaIds` array at least one of the distributions has to be more than `0`
9. Lengths of distribution arrays and delta ID array have to be the same
10. Maximum number of bins, that can be populated at the same time is around `51` due to AVAX gas block limit (`8M`) 
11. If you want to add liquidity only to one side, use `amountX = 0` or `amountX = 0` and appropriate `_deltaIds`

#### Code sample

```js
uint256 PRECISION = 1e18;
uint256 binStep = 25; 
uint256 _amountX = 100 * 10e6; 
uint256 _amountY = 100 * 10e18;
uint256 _amountXmin = 99 * 10e6; //allow 1% amount slippage
uint256 _amountYmin = 99 * 10e18; //allow 1% amount slippage

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
    token6D,
    token18D,
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

//fund your account with test tokens and approve spending by router
token6D.mint(DEV, _amountX);
token18D.mint(DEV, _amountY);
token6D.approve(address(router), _amountX);
token18D.approve(address(router), _amountY);

(uint256[] memory depositIds, uint256[] memory liquidityMinted) = router.addLiquidity(_liquidityParameters);
```


Some distribution examples (on very small sample sizes):
1. Deposit only token X, above current price. If price moves in desired direction, tokenY + accrued fees can be withdrawn from every bin independently - DCA strategy
```
_deltaIds = [1, 11, 33],  
_distributionX = [PRECISION / 3, PRECISION / 3, PRECISION / 3], 
_amountY & _amountYmin = 0
```

2. Deposit all tokens to single bin - maximum capital concentration; no more fees will be accrued if active bin changes
```
_deltaIds = [0], 
_distributionX = [PRECISION],
_distributionY = [PRECISION]
```

3. Deposit tokens to earn fees only during high volatility of stable pair. No fees earned while `priceX ~ priceY`, high fees accrued while price deviates.
```
_deltaIds = [-5, 5],  
_distributionX = [0, PRECISION], 
_distributionY = [PRECISION, 0]
```

