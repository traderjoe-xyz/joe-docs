---
sidebar_position: 9
sidebar_label: IJoeRouter02
---

## IJoeRouter02

Interface to interact with Joe V1 Router

### removeLiquidityAVAXSupportingFeeOnTransferTokens

```solidity
function removeLiquidityAVAXSupportingFeeOnTransferTokens(address token, uint256 liquidity, uint256 amountTokenMin, uint256 amountAVAXMin, address to, uint256 deadline) external returns (uint256 amountAVAX)
```

### removeLiquidityAVAXWithPermitSupportingFeeOnTransferTokens

```solidity
function removeLiquidityAVAXWithPermitSupportingFeeOnTransferTokens(address token, uint256 liquidity, uint256 amountTokenMin, uint256 amountAVAXMin, address to, uint256 deadline, bool approveMax, uint8 v, bytes32 r, bytes32 s) external returns (uint256 amountAVAX)
```

### swapExactTokensForTokensSupportingFeeOnTransferTokens

```solidity
function swapExactTokensForTokensSupportingFeeOnTransferTokens(uint256 amountIn, uint256 amountOutMin, address[] path, address to, uint256 deadline) external
```

### swapExactAVAXForTokensSupportingFeeOnTransferTokens

```solidity
function swapExactAVAXForTokensSupportingFeeOnTransferTokens(uint256 amountOutMin, address[] path, address to, uint256 deadline) external payable
```

### swapExactTokensForAVAXSupportingFeeOnTransferTokens

```solidity
function swapExactTokensForAVAXSupportingFeeOnTransferTokens(uint256 amountIn, uint256 amountOutMin, address[] path, address to, uint256 deadline) external
```

