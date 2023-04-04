## Uint256x256 Math 

Helper contract used for full precision calculations

### mulDivRoundDown

```solidity
function mulDivRoundDown(uint256 x, uint256 y, uint256 denominator) internal pure returns (uint256 result)
```

Calculates `floor(x*y/denominator)` with full precision. The result will be rounded down.

Requirements:
- The denominator cannot be zero
- The result must fit within uint256

Caveats:
- This function does not work with fixed-point numbers

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| x | uint256 | The multiplicand as an uint256 |
| y | uint256 | The multiplier as an uint256 |
| denominator | uint256 | The divisor as an uint256 |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| [0] | uint256 | The result as an uint256 |

### mulDivRoundUp

```solidity
function mulDivRoundUp(uint256 x, uint256 y, uint256 denominator) internal pure returns (uint256 result)
```

Calculates `ceil(x*y/denominator)` with full precision. The result will be rounded up.

Requirements:
- The denominator cannot be zero
- The result must fit within uint256

Caveats:
- This function does not work with fixed-point numbers

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| x | uint256 | The multiplicand as an uint256 |
| y | uint256 | The multiplier as an uint256 |
| denominator | uint256 | The divisor as an uint256 |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| [0] | uint256 | The result as an uint256 |

### mulShiftRoundDown

```solidity
function mulShiftRoundDown(uint256 x, uint256 y, uint8 offset) internal pure returns (uint256 result)
```

Calculates `floor(x * y / 2**offset)` with full precision. The result will be rounded down.

Requirements:
- The offset needs to be strictly lower than 256
- The result must fit within uint256

Caveats:
- This function does not work with fixed-point numbers

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| x | uint256 | The multiplicand as an uint256 |
| y | uint256 | The multiplier as an uint256 |
| offset | uint8 | The offset as an uint256, can't be greater than 256 |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| [0] | uint256 | The result as an uint256 |

### mulShiftRoundUp

```solidity
function mulShiftRoundUp(uint256 x, uint256 y, uint8 offset) internal pure returns (uint256 result)
```

Calculates `ceil(x * y / 2**offset)` with full precision. The result will be rounded up.

Requirements:
- The offset needs to be strictly lower than 256
- The result must fit within uint256

Caveats:
- This function does not work with fixed-point numbers

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| x | uint256 | The multiplicand as an uint256 |
| y | uint256 | The multiplier as an uint256 |
| offset | uint8 | The offset as an uint256, can't be greater than 256 |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| [0] | uint256 | The result as an uint256 |

### shiftDivRoundDown

```solidity
function shiftDivRoundDown(uint256 x, uint8 offset, uint256 denominator) internal pure returns (uint256 result)
```

Calculates `floor(x << offset / y)` with full precision. The result will be rounded down.

Requirements:
- The offset needs to be strictly lower than 256
- The result must fit within uint256

Caveats:
- This function does not work with fixed-point numbers

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| x | uint256 | The multiplicand as an uint256 |
| offset | uint8 | The number of bit to shift x as an uint256 |
| denominator | uint256 | The divisor as an uint256 |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| [0] | uint256 | The result as an uint256 |

### shiftDivRoundUp

```solidity
function shiftDivRoundUp(uint256 x, uint8 offset, uint256 denominator) internal pure returns (uint256 result)
```

Calculates ceil(x << offset / y) with full precision
The result will be rounded up

Requirements:
- The offset needs to be strictly lower than 256
- The result must fit within uint256

Caveats:
- This function does not work with fixed-point numbers

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| x | uint256 | The multiplicand as an uint256 |
| offset | uint8 | The number of bit to shift x as an uint256 |
| denominator | uint256 | The divisor as an uint256 |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| [0] | uint256 | The result as an uint256 |

### _getMulProds

```solidity
function _getMulProds(uint256 x, uint256 y) private pure returns (uint256 prod0, uint256 prod1)
```

Helper function to return the result of `x * y` as 2 uint256

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| x | uint256 | The multiplicand as an uint256 |
| y | uint256 | The multiplier as an uint256 |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| prod0 | uint256 | The least significant 256 bits of the product |
| prod1 | uint256 | The most significant 256 bits of the product |

### _getEndOfDivRoundDown

```solidity
function _getEndOfDivRoundDown(uint256 x, uint256 y, uint256 denominator, uint256 prod0, uint256 prod1) private pure returns (uint256 result)
```

Helper function to return the result of `x * y / denominator` with full precision

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| x | uint256 | The multiplicand as an uint256 |
| y | uint256 | The multiplier as an uint256 |
| denominator | uint256 | The divisor as an uint256 |
| prod0 | uint256 | The least significant 256 bits of the product |
| prod1 | uint256 | The most significant 256 bits of the product |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| [0] | uint256 | The result as an uint256 |