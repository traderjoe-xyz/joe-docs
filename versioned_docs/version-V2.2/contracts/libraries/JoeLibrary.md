## Joe Library

Helper contract used for Joe V1 related calculations

### sortTokens

```solidity
function sortTokens(address tokenA, address tokenB) internal pure returns (address token0, address token1)
```

returns sorted token addresses, used to handle return values from pairs sorted in this order

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| tokenA | address | The first token address |
| tokenB | address | The second token address |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| token0 | address | The address of the first sorted token |
| token1 | address | The address of the second sorted token |

### quote

```solidity
function quote(uint256 amountA, uint256 reserveA, uint256 reserveB) internal pure returns (uint256 amountB)
```

given some amount of an asset and pair reserves, returns an equivalent amount of the other asset

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| amountA | uint256 | The amount of asset A |
| reserveA | uint256 | The reserve of asset A |
| reserveB | uint256 | The reserve of asset B |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| amountB | uint256 | The equivalent amount of asset B |

### getAmountOut

```solidity
function getAmountOut(uint256 amountIn, uint256 reserveIn, uint256 reserveOut) internal pure returns (uint256 amountOut)
```

given an input amount of an asset and pair reserves, returns the maximum output amount of the other asset

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| amountIn | uint256 | The input amount of an asset |
| reserveIn | uint256 | The reserve of input asset |
| reserveOut | uint256 | The reserve of output asset |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| amountOut | uint256 | The maximum output amount of the other asset |

### getAmountIn

```solidity
function getAmountIn(uint256 amountOut, uint256 reserveIn, uint256 reserveOut) internal pure returns (uint256 amountIn)
```

given an output amount of an asset and pair reserves, returns a required input amount of the other asset

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| amountOut | uint256 | The output amount of an asset |
| reserveIn | uint256 | The reserve of input asset |
| reserveOut | uint256 | The reserve of output asset |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| amountIn | uint256 | The required input amount of the other asset |