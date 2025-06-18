# JoeLibrary
[Git Source](https://github.com/lfj-gg/joe-v2/blob/16f011d25e6bf6d0a0c479974345b623d491104f/src/libraries/JoeLibrary.sol)

**Author:**
Trader Joe

Helper contract used for Joe V1 related calculations


## Functions
### sortTokens


```solidity
function sortTokens(address tokenA, address tokenB) internal pure returns (address token0, address token1);
```

### quote


```solidity
function quote(uint256 amountA, uint256 reserveA, uint256 reserveB) internal pure returns (uint256 amountB);
```

### getAmountOut


```solidity
function getAmountOut(uint256 amountIn, uint256 reserveIn, uint256 reserveOut)
    internal
    pure
    returns (uint256 amountOut);
```

### getAmountIn


```solidity
function getAmountIn(uint256 amountOut, uint256 reserveIn, uint256 reserveOut)
    internal
    pure
    returns (uint256 amountIn);
```

## Errors
### JoeLibrary__AddressZero

```solidity
error JoeLibrary__AddressZero();
```

### JoeLibrary__IdenticalAddresses

```solidity
error JoeLibrary__IdenticalAddresses();
```

### JoeLibrary__InsufficientAmount

```solidity
error JoeLibrary__InsufficientAmount();
```

### JoeLibrary__InsufficientLiquidity

```solidity
error JoeLibrary__InsufficientLiquidity();
```

