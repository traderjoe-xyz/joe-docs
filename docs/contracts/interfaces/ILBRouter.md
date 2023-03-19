## ILBRouter

Required interface of LBRouter contract

### Version

```solidity
enum Version{
    V1,
    V2,
    V2_1
}
```
This enum represents the version of the pair requested: <br/>
* V1: Joe V1 pair
* V2: LB pair V2. Also called legacyPair
* V2_1: LB pair V2.1 (current version)

### LiquidityParameters

```solidity
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
    address refundTo;
    uint256 deadline;
}
```

The liquidity parameters, such as: <br/>
* tokenX: The address of token X
* tokenY: The address of token Y
* binStep: The bin step of the pair
* amountX: The amount to send of token X
* amountY: The amount to send of token Y
* amountXMin: The min amount of token X added to liquidity
* amountYMin: The min amount of token Y added to liquidity
* activeIdDesired: The active id that user wants to add liquidity from
* idSlippage: The number of id that are allowed to slip
* deltaIds: The list of delta ids to add liquidity (`deltaId = activeId - desiredId`)
* distributionX: The distribution of tokenX with sum(distributionX) = 100e18 (100%) or 0 (0%)
* distributionY: The distribution of tokenY with sum(distributionY) = 100e18 (100%) or 0 (0%)
* to: The address of the recipient
* deadline: The deadline of the tx

### Path

```solidity
struct Path{
    uint256[] pairBinSteps;
    Version[] versions;
    IERC20[] tokenPath;
}
```

The path parameters, such as:
* pairBinSteps: The list of bin steps of the pairs to go through
* versions: The list of versions of the pairs to go through
* tokenPath: The list of tokens in the path to go through


### getFactory

```solidity
function getFactory() external view override returns (ILBFactory lbFactory)
```

### getLegacyFactory

```solidity
function getLegacyFactory() external view override returns (ILBLegacyFactory legacyLBfactory)
```


### getV1Factory

```solidity
function getV1Factory() external view override returns (IJoeFactory factoryV1)
```


### getLegacyRouter

```solidity
function getLegacyRouter() external view override returns (ILBLegacyRouter legacyRouter)
```

### getWNATIVE

```solidity
function getWNATIVE() external view override returns (IWNATIVE wnative)
```

### getIdFromPrice

```solidity
function getIdFromPrice(ILBPair pair, uint256 price) external view override returns (uint24)
```

### getPriceFromId

```solidity
function getPriceFromId(ILBPair pair, uint24 id) external view override returns (uint256)
```

### getSwapIn

```solidity
function getSwapIn(ILBPair pair, uint128 amountOut, bool swapForY) public view override returns (uint128 amountIn, uint128 amountOutLeft, uint128 fee)
```

### getSwapOut

```solidity
function getSwapOut(ILBPair pair, uint128 amountIn, bool swapForY) external view override returns (uint128 amountInLeft, uint128 amountOut, uint128 fee)
```

### createLBPair

```solidity
function createLBPair(IERC20 tokenX, IERC20 tokenY, uint24 activeId, uint16 binStep) external override returns (ILBPair pair)
```

### addLiquidity

```solidity
function addLiquidity(
    LiquidityParameters calldata liquidityParameters
) external returns (
    uint256 amountXAdded,
    uint256 amountYAdded,
    uint256 amountXLeft,
    uint256 amountYLeft,
    uint256[] memory depositIds,
    uint256[] memory liquidityMinted
)
```

### addLiquidityNATIVE

```solidity
function addLiquidityNATIVE(
    LiquidityParameters calldata liquidityParameters
) external payable returns (
    uint256 amountXAdded,
    uint256 amountYAdded,
    uint256 amountXLeft,
    uint256 amountYLeft,
    uint256[] memory depositIds,
    uint256[] memory liquidityMinted
)
```

### removeLiquidity

```solidity
function removeLiquidity(
    IERC20 tokenX,
    IERC20 tokenY,
    uint16 binStep,
    uint256 amountXMin,
    uint256 amountYMin,
    uint256[] memory ids,
    uint256[] memory amounts,
    address to,
    uint256 deadline
) external ensure(deadline) returns (uint256 amountX, uint256 amountY)
```

### removeLiquidityNATIVE

```solidity
function removeLiquidityNATIVE(
    IERC20 token,
    uint16 binStep,
    uint256 amountTokenMin,
    uint256 amountNATIVEMin,
    uint256[] memory ids,
    uint256[] memory amounts,
    address payable to,
    uint256 deadline
) external ensure(deadline) returns (uint256 amountToken, uint256 amountNATIVE)
```

### swapExactTokensForTokens

```solidity
function swapExactTokensForTokens(
    uint256 amountIn,
    uint256 amountOutMin,
    Path memory path,
    address to,
    uint256 deadline
) external ensure(deadline) verifyPathValidity(path) returns (uint256 amountOut)
```

### swapExactTokensForNATIVE

```solidity
function swapExactTokensForNATIVE(uint256 amountIn, uint256 amountOutMinNATIVE, Path memory path, address payable to, uint256 deadline) external override ensure(deadline) verifyPathValidity(path) returns (uint256 amountOut)
```

### swapExactNATIVEForTokens

```solidity
function swapExactNATIVEForTokens(uint256 amountOutMin, Path memory path, address to, uint256 deadline) external payable override ensure(deadline) verifyPathValidity(path) returns (uint256 amountOut)
```

### swapTokensForExactTokens

```solidity
function swapTokensForExactTokens(uint256 amountOut, uint256 amountInMax, Path memory path, address to, uint256 deadline) external override ensure(deadline) verifyPathValidity(path) returns (uint256[] memory amountsIn)
```

### swapTokensForExactNATIVE

```solidity
function swapTokensForExactNATIVE(uint256 amountNATIVEOut, uint256 amountInMax, Path memory path, address payable to, uint256 deadline) external override ensure(deadline) verifyPathValidity(path) returns (uint256[] memory amountsIn)
```

Swaps tokens for exact NATIVE while performing safety checks


### swapNATIVEForExactTokens

```solidity
function swapNATIVEForExactTokens(uint256 amountOut, Path memory path, address to, uint256 deadline) external payable override ensure(deadline) verifyPathValidity(path) returns (uint256[] memory amountsIn)
```

### swapExactTokensForTokensSupportingFeeOnTransferTokens

```solidity
function swapExactTokensForTokensSupportingFeeOnTransferTokens(uint256 amountIn, uint256 amountOutMin, Path memory path, address to, uint256 deadline) external override ensure(deadline) verifyPathValidity(path) returns (uint256 amountOut)
```

### swapExactTokensForNATIVESupportingFeeOnTransferTokens

```solidity
function swapExactTokensForNATIVESupportingFeeOnTransferTokens(uint256 amountIn, uint256 amountOutMinNATIVE, Path memory path, address payable to, uint256 deadline) external override ensure(deadline) verifyPathValidity(path) returns (uint256 amountOut)
```

### swapExactNATIVEForTokensSupportingFeeOnTransferTokens

```solidity
function swapExactNATIVEForTokensSupportingFeeOnTransferTokens(uint256 amountOutMin, Path memory path, address to, uint256 deadline) external payable override ensure(deadline) verifyPathValidity(path) returns (uint256 amountOut)
```

### sweep

```solidity
function sweep(IERC20 token, address to, uint256 amount) external override onlyFactoryOwner
```

### sweepLBToken

```solidity
function sweepLBToken(ILBToken lbToken, address to, uint256[] calldata ids, uint256[] calldata amounts) external override onlyFactoryOwner
```