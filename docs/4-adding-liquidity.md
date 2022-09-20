---
id: Adding Liquidity
---

To add liquidity using router struct `LiquidityParameters` from `ILBRouter.sol` should be used.

```js
struct LiquidityParameters {
    IERC20 tokenX;
    IERC20 tokenY;
    uint256 binStep;
    uint256 amountX;
    uint256 amountY;
    uint256 amountXMin;
    uint256 amountYMin;
    uint256 activeIdDesired;
    uint256 idSlippage;
    int256[] deltaIds;
    uint256[] distributionX;
    uint256[] distributionY;
    address to;
    uint256 deadline;
}
```


```js
uint256 PRECISION = 1e18; //defined in Constants.sol
uint256 binStep = 25; //has to point to existing pair
uint256 _amountX = 100 * 10e6; //amount that you want to add to liquidity
uint256 _amountY = 100 * 10e18; //amount that you want to add to liquidity
uint256 _amountXmin = 99 * 10e6; //allow 1% amount slippage while adding liquidity
uint256 _amountYmin = 99 * 10e18; //allow 1% amount slippage while adding liquidity
//in practice amount slippage will never be significant if distributions are set properly
uint256 _activeIdDesired = 2**23; //currently active bin
uint256 _idSlippage = 5; //if price (active bin) moves more than that, transaction will revert

//more info about distribution/delta IDs below
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


Distributions + delta IDs define, how tokens will be spread across bins.
Liquidity deposited is always dependent on currently active bin.

Take below points into account while choosing LiquidityParameters:
1. Sum of all values in _distributionX array has to be less or equal to Constants.PRECISION
2. Sum of all values in _distributionY array has to be less or equal to Constants.PRECISION
3. Distributions can take all shapes and values, and are set independently.
4. If sum of all distributions is not equal to Constants.PRECISION, you will not deposit full _amountX/_amountY value. Plan _amountXmin/_amountYmin accordingly.
5. _distributionX for IDs < _activeIdDesired has to be 0
6. _distributionY for IDs > _activeIdDesired has to be 0
7. Length of distribution arrays and deltaIDs array has to be the same
8. Maximum number of bins, that can be populated at the same time is around 51 due to AVAX gas block limit (8M) 
9. If you want to add liquidity only to one side, use _amountX/_amountY = 0 and appropriate _deltaIds

Some distribution examples (on very small sample sizes):
1. Deposit only token X, above current price. If price moves in desired direction, you can withdraw tokenY + accrued fees, from every bin independently - DCA strategy
```
_deltaIds = [1, 11, 33],  
_distributionX = [PRECISION / 3, PRECISION / 3, PRECISION / 3], 
_amountY & _amountYmin = 0
```

2. Deposit all tokens to single bin - maximum capital concentration; no fees if active bin changes
```
_deltaIds = [0], 
_distributionX = [PRECISION],
_distributionX = [PRECISION]
```

3. Deposit tokens to earn fees only during high volatility of stable pair. No fees earned while `priceX ~ priceY`, high fees accrued while price deviates.
```
_deltaIds = [-5, 5],  
_distributionX = [0, PRECISION], 
_distributionY = [PRECISION, 0]
```

