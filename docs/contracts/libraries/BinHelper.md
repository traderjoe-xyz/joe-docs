## Bin Helper

This library contains functions to help interaction with bins.

### getAmountOutOfBin

```solidity
function getAmountOutOfBin(bytes32 binReserves, uint256 amountToBurn, uint256 totalSupply) internal pure returns (bytes32 amountsOut)
```

Returns the amount of tokens that will be received when burning the given amount of liquidity

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| binReserves | bytes32 | The reserves of the bin |
| amountToBurn | uint256 | The amount of liquidity to burn |
| totalSupply | uint256 | The total supply of the liquidity book |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| amountsOut | bytes32 | The encoded amount of tokens that will be received |

### getSharesAndEffectiveAmountsIn

```solidity
function getSharesAndEffectiveAmountsIn(bytes32 binReserves, bytes32 amountsIn, uint256 price, uint256 totalSupply) internal pure returns (uint256 shares, bytes32 effectiveAmountsIn)
```

Returns the share and the effective amounts in when adding liquidity

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| binReserves | bytes32 | The reserves of the bin |
| amountsIn | bytes32 | The amounts of tokens to add |
| price | uint256 | The price of the bin |
| totalSupply | uint256 | The total supply of the liquidity book |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| shares | uint256 | The share of the liquidity book that the user will receive |
| effectiveAmountsIn | bytes32 | The encoded effective amounts of tokens that the user will add. This is the amount of tokens that the user will actually add to the liquidity book, and will always be less than or equal to the amountsIn. |

### getLiquidity

```solidity
function getLiquidity(bytes32 amounts, uint256 price) internal pure returns (uint256 liquidity)
```

Returns the amount of liquidity following the constant sum formula `L = price * x + y`

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| amounts | bytes32 | The amounts of tokens |
| price | uint256 | The price of the bin |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| liquidity | uint256 | The amount of liquidity |

### verifyAmounts

```solidity
function verifyAmounts(bytes32 amounts, uint24 activeId, uint24 id) internal pure
```

Verify that the amounts are correct and that the composition factor is not flawed

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| amounts | bytes32 | The amounts of tokens |
| activeId | uint24 | The id of the active bin |
| id | uint24 | The id of the bin |

### getCompositionFees

```solidity
function getCompositionFees(bytes32 binReserves, bytes32 parameters, uint16 binStep, bytes32 amountsIn, uint256 totalSupply, uint256 shares) internal pure returns (bytes32 fees)
```

Returns the composition fees when adding liquidity to the active bin with a different composition factor than the bin's one, as it does an implicit swap

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| binReserves | bytes32 | The reserves of the bin |
| parameters | bytes32 | The parameters of the liquidity book |
| binStep | uint16 | The step of the bin |
| amountsIn | bytes32 | The amounts of tokens to add |
| totalSupply | uint256 | The total supply of the liquidity book |
| shares | uint256 | The share of the liquidity book that the user will receive |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| fees | bytes32 | The encoded fees that will be charged |

### isEmpty

```solidity
function isEmpty(bytes32 binReserves, bool isX) internal pure returns (bool)
```

Returns whether the bin is empty (true) or not (false)

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| binReserves | bytes32 | The reserves of the bin |
| isX | bool | Whether the reserve to check is the X reserve (true) or the Y reserve (false) |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
|  | bool | Whether the bin is empty (true) or not (false) |

### getAmounts

```solidity
function getAmounts(bytes32 binReserves, bytes32 parameters, uint16 binStep, bool swapForY, uint24 activeId, bytes32 amountsInLeft) internal pure returns (bytes32 amountsInWithFees, bytes32 amountsOutOfBin, bytes32 totalFees)
```

Returns the amounts of tokens that will be added and removed from the bin during a swap along with the fees that will be charged

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| binReserves | bytes32 | The reserves of the bin |
| parameters | bytes32 | The parameters of the liquidity book |
| binStep | uint16 | The step of the bin |
| swapForY | bool | Whether the swap is for Y (true) or for X (false) |
| activeId | uint24 | The id of the active bin |
| amountsInLeft | bytes32 | The amounts of tokens left to swap |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| amountsInWithFees | bytes32 | The encoded amounts of tokens that will be added to the bin, including fees |
| amountsOutOfBin | bytes32 | The encoded amounts of tokens that will be removed from the bin |
| totalFees | bytes32 | The encoded fees that will be charged |

### received

```solidity
function received(bytes32 reserves, IERC20 tokenX, IERC20 tokenY) internal view returns (bytes32 amounts)
```

Returns the encoded amounts that was transferred to the contract

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| reserves | bytes32 | The reserves |
| tokenX | IERC20 | The token X |
| tokenY | IERC20 | The token Y |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| amounts | bytes32 | The amounts, encoded as follows:<br/>[0 - 128[: amountX<br/>[128 - 256[: amountY |

### receivedX

```solidity
function receivedX(bytes32 reserves, IERC20 tokenX) internal view returns (bytes32)
```

Returns the encoded amounts that was transferred to the contract, only for token X

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| reserves | bytes32 | The reserves |
| tokenX | IERC20 | The token X |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
|  | bytes32 | The amounts, encoded as follows:<br/>[0 - 128[: amountX<br/>[128 - 256[: empty |

### receivedY

```solidity
function receivedY(bytes32 reserves, IERC20 tokenY) internal view returns (bytes32)
```

Returns the encoded amounts that was transferred to the contract, only for token Y

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| reserves | bytes32 | The reserves |
| tokenY | IERC20 | The token Y |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
|  | bytes32 | The amounts, encoded as follows:<br/>[0 - 128[: empty<br/>[128 - 256[: amountY |

### transfer

```solidity
function transfer(bytes32 amounts, IERC20 tokenX, IERC20 tokenY, address recipient) internal
```

Transfers the encoded amounts to the recipient

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| amounts | bytes32 | The amounts, encoded as follows:<br/>[0 - 128[: amountX<br/>[128 - 256[: amountY |
| tokenX | IERC20 | The token X |
| tokenY | IERC20 | The token Y |
| recipient | address | The recipient |

### transferX

```solidity
function transferX(bytes32 amounts, IERC20 tokenX, address recipient) internal
```

Transfers the encoded amounts to the recipient, only for token X

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| amounts | bytes32 | The amounts, encoded as follows:<br/>[0 - 128[: amountX<br/>[128 - 256[: empty |
| tokenX | IERC20 | The token X |
| recipient | address | The recipient |

### transferY

```solidity
function transferY(bytes32 amounts, IERC20 tokenY, address recipient) internal
```

Transfers the encoded amounts to the recipient, only for token Y

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| amounts | bytes32 | The amounts, encoded as follows:<br/>[0 - 128[: empty<br/>[128 - 256[: amountY |
| tokenY | IERC20 | The token Y |
| recipient | address | The recipient |

### _balanceOf

```solidity
function _balanceOf(IERC20 token) private view returns (uint128)
```

Returns the balance of the specified token in the contract

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| token | IERC20 | The token |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
|  | uint128 | The balance of the specified token in the contract |