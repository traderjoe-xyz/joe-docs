## LBQuoter

Helper contract to determine best path through multiple markets

### constructor 

```solidity
constructor(address factoryV1, address legacyFactoryV2, address factoryV2, address legacyRouterV2, address routerV2) 
```

Constructor

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| factoryV1 | address | Dex V1 factory address |
| legacyFactoryV2 | address | Dex V2 factory address |
| factoryV2 | address | Dex V2.1 factory address |
| legacyRouterV2 | address | Dex V2 router address |
| routerV2 | address | Dex V2 router address |

### getFactoryV1

```solidity
function getFactoryV1() external view returns (address factoryV1)
```

Returns the Dex V1 factory address

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| factoryV1 | address | Dex V1 factory address |

### getLegacyFactoryV2

```solidity
function getLegacyFactoryV2() external view returns (address legacyFactoryV2)
```

Returns the Dex V2 factory address

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| legacyFactoryV2 | address | Dex V2 factory address |

### getFactoryV2

```solidity
function getFactoryV2() external view returns (address factoryV2)
```

Returns the Dex V2.1 factory address

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| factoryV2 | address | Dex V2.1 factory address |

### getLegacyRouterV2

```solidity
function getLegacyRouterV2() external view returns (address legacyRouterV2)
```

Returns the Dex V2 router address

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| legacyRouterV2 | address | Dex V2 router address |

### getRouterV2

```solidity
function getRouterV2() external view returns (address routerV2)
```

Returns the Dex V2 router address

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| routerV2 | address | Dex V2 router address |

### findBestPathFromAmountIn

```solidity
function findBestPathFromAmountIn(address[] calldata route, uint128 amountIn) public view returns (Quote memory quote)
```

Finds the best path given a list of tokens and the input amount wanted from the swap

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| `route` | `address[]` | List of the tokens to go through |
| `amountIn` | `uint128` | Swap amount in |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| `quote` | `Quote` | The Quote structure containing the necessary element to perform the swap |

### findBestPathFromAmountOut

```solidity
function findBestPathFromAmountOut(address[] calldata route, uint128 amountOut) public view returns (Quote memory quote)
```

Finds the best path given a list of tokens and the output amount wanted from the swap

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| route | address[] calldata | List of the tokens to go through |
| amountOut | uint128 | Swap amount out |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| quote | Quote memory | The Quote structure containing the necessary element to perform the swap |

### _getReserves

```solidity
function _getReserves(address pair, address tokenA, address tokenB) internal view returns (uint256 reserveA, uint256 reserveB)
```

Calculates the pair reserves 

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| pair | address | Address of the pair |
| tokenA | address | Address of token A |
| tokenB | address | Address of token B |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| reserveA | uint256 | Reserve of token A in the pair |
| reserveB | uint256 | Reserve of token B in the pair |

### _getV2Quote

```solidity
function _getV2Quote(uint256 amount, uint24 activeId, uint256 binStep, bool swapForY) internal pure returns (uint128 quote)
```

Calculates the amount out for a V2 pair

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| amount | uint256 | Amount in to consider |
| activeId | uint24 | Current active Id of the considered pair |
| binStep | uint256 | Bin step of the considered pair |
| swapForY | bool | Boolean describing if we are swapping from X to Y or the opposite |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| quote | uint128 | Amount Out if _amount was swapped with no slippage and no fees |