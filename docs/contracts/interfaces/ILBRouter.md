---
sidebar_position: 0
sidebar_label: 
---

## ILBRouter

Required interface of LBRouter contract

### LiquidityParameters

```solidity
struct LiquidityParameters {
  contract IERC20 tokenX;
  contract IERC20 tokenY;
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

### factory

```solidity
function factory() external view returns (contract ILBFactory)
```

### oldFactory

```solidity
function oldFactory() external view returns (contract IJoeFactory)
```

### wavax

```solidity
function wavax() external view returns (contract IWAVAX)
```

### getIdFromPrice

```solidity
function getIdFromPrice(contract ILBPair LBPair, uint256 price) external view returns (uint24)
```

### getPriceFromId

```solidity
function getPriceFromId(contract ILBPair LBPair, uint24 id) external view returns (uint256)
```

### getSwapIn

```solidity
function getSwapIn(contract ILBPair LBPair, uint256 amountOut, bool swapForY) external view returns (uint256 amountIn, uint256 feesIn)
```

### getSwapOut

```solidity
function getSwapOut(contract ILBPair LBPair, uint256 amountIn, bool swapForY) external view returns (uint256 amountOut, uint256 feesIn)
```

### createLBPair

```solidity
function createLBPair(contract IERC20 tokenX, contract IERC20 tokenY, uint24 activeId, uint16 binStep) external returns (contract ILBPair pair)
```

### addLiquidity

```solidity
function addLiquidity(struct ILBRouter.LiquidityParameters liquidityParameters) external returns (uint256[] depositIds, uint256[] liquidityMinted)
```

### addLiquidityAVAX

```solidity
function addLiquidityAVAX(struct ILBRouter.LiquidityParameters liquidityParameters) external payable returns (uint256[] depositIds, uint256[] liquidityMinted)
```

### removeLiquidity

```solidity
function removeLiquidity(contract IERC20 tokenX, contract IERC20 tokenY, uint16 binStep, uint256 amountXMin, uint256 amountYMin, uint256[] ids, uint256[] amounts, address to, uint256 deadline) external returns (uint256 amountX, uint256 amountY)
```

### removeLiquidityAVAX

```solidity
function removeLiquidityAVAX(contract IERC20 token, uint16 binStep, uint256 amountTokenMin, uint256 amountAVAXMin, uint256[] ids, uint256[] amounts, address payable to, uint256 deadline) external returns (uint256 amountToken, uint256 amountAVAX)
```

### swapExactTokensForTokens

```solidity
function swapExactTokensForTokens(uint256 amountIn, uint256 amountOutMin, uint256[] pairBinSteps, contract IERC20[] tokenPath, address to, uint256 deadline) external returns (uint256 amountOut)
```

### swapExactTokensForAVAX

```solidity
function swapExactTokensForAVAX(uint256 amountIn, uint256 amountOutMinAVAX, uint256[] pairBinSteps, contract IERC20[] tokenPath, address payable to, uint256 deadline) external returns (uint256 amountOut)
```

### swapExactAVAXForTokens

```solidity
function swapExactAVAXForTokens(uint256 amountOutMin, uint256[] pairBinSteps, contract IERC20[] tokenPath, address to, uint256 deadline) external payable returns (uint256 amountOut)
```

### swapTokensForExactTokens

```solidity
function swapTokensForExactTokens(uint256 amountOut, uint256 amountInMax, uint256[] pairBinSteps, contract IERC20[] tokenPath, address to, uint256 deadline) external returns (uint256[] amountsIn)
```

### swapTokensForExactAVAX

```solidity
function swapTokensForExactAVAX(uint256 amountOut, uint256 amountInMax, uint256[] pairBinSteps, contract IERC20[] tokenPath, address payable to, uint256 deadline) external returns (uint256[] amountsIn)
```

### swapAVAXForExactTokens

```solidity
function swapAVAXForExactTokens(uint256 amountOut, uint256[] pairBinSteps, contract IERC20[] tokenPath, address to, uint256 deadline) external payable returns (uint256[] amountsIn)
```

### swapExactTokensForTokensSupportingFeeOnTransferTokens

```solidity
function swapExactTokensForTokensSupportingFeeOnTransferTokens(uint256 amountIn, uint256 amountOutMin, uint256[] pairBinSteps, contract IERC20[] tokenPath, address to, uint256 deadline) external returns (uint256 amountOut)
```

### swapExactTokensForAVAXSupportingFeeOnTransferTokens

```solidity
function swapExactTokensForAVAXSupportingFeeOnTransferTokens(uint256 amountIn, uint256 amountOutMinAVAX, uint256[] pairBinSteps, contract IERC20[] tokenPath, address payable to, uint256 deadline) external returns (uint256 amountOut)
```

### swapExactAVAXForTokensSupportingFeeOnTransferTokens

```solidity
function swapExactAVAXForTokensSupportingFeeOnTransferTokens(uint256 amountOutMin, uint256[] pairBinSteps, contract IERC20[] tokenPath, address to, uint256 deadline) external payable returns (uint256 amountOut)
```

### sweep

```solidity
function sweep(contract IERC20 token, address to, uint256 amount) external
```

### sweepLBToken

```solidity
function sweepLBToken(contract ILBToken _lbToken, address _to, uint256[] _ids, uint256[] _amounts) external
```

