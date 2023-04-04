---
sidebar_position: 0
sidebar_label: Math512Bits
---

## Math512Bits

Helper contract used for full precision calculations

### mulDivRoundDown

```solidity
function mulDivRoundDown(uint256 x, uint256 y, uint256 denominator) internal pure returns (uint256 result)
```

Calculates floor(x*y÷denominator) with full precision
The result will be rounded down

_Credit to Remco Bloemen under MIT license https://xn--2-umb.com/21/muldiv

Requirements:
- The denominator cannot be zero
- The result must fit within uint256

Caveats:
- This function does not work with fixed-point numbers_

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| x | uint256 | The multiplicand as an uint256 |
| y | uint256 | The multiplier as an uint256 |
| denominator | uint256 | The divisor as an uint256 |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| result | uint256 | The result as an uint256 |

### mulShiftRoundDown

```solidity
function mulShiftRoundDown(uint256 x, uint256 y, uint256 offset) internal pure returns (uint256 result)
```

Calculates x * y >> offset with full precision
The result will be rounded down

_Credit to Remco Bloemen under MIT license https://xn--2-umb.com/21/muldiv

Requirements:
- The offset needs to be strictly lower than 256
- The result must fit within uint256

Caveats:
- This function does not work with fixed-point numbers_

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| x | uint256 | The multiplicand as an uint256 |
| y | uint256 | The multiplier as an uint256 |
| offset | uint256 | The offset as an uint256, can't be greater than 256 |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| result | uint256 | The result as an uint256 |

### mulShiftRoundUp

```solidity
function mulShiftRoundUp(uint256 x, uint256 y, uint256 offset) internal pure returns (uint256 result)
```

Calculates x * y >> offset with full precision
The result will be rounded up

_Credit to Remco Bloemen under MIT license https://xn--2-umb.com/21/muldiv

Requirements:
- The offset needs to be strictly lower than 256
- The result must fit within uint256

Caveats:
- This function does not work with fixed-point numbers_

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| x | uint256 | The multiplicand as an uint256 |
| y | uint256 | The multiplier as an uint256 |
| offset | uint256 | The offset as an uint256, can't be greater than 256 |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| result | uint256 | The result as an uint256 |

### shiftDivRoundDown

```solidity
function shiftDivRoundDown(uint256 x, uint256 offset, uint256 denominator) internal pure returns (uint256 result)
```

Calculates x << offset / y with full precision
The result will be rounded down

_Credit to Remco Bloemen under MIT license https://xn--2-umb.com/21/muldiv

Requirements:
- The offset needs to be strictly lower than 256
- The result must fit within uint256

Caveats:
- This function does not work with fixed-point numbers_

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| x | uint256 | The multiplicand as an uint256 |
| offset | uint256 | The number of bit to shift x as an uint256 |
| denominator | uint256 | The divisor as an uint256 |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| result | uint256 | The result as an uint256 |

### shiftDivRoundUp

```solidity
function shiftDivRoundUp(uint256 x, uint256 offset, uint256 denominator) internal pure returns (uint256 result)
```

Calculates x << offset / y with full precision
The result will be rounded up

_Credit to Remco Bloemen under MIT license https://xn--2-umb.com/21/muldiv

Requirements:
- The offset needs to be strictly lower than 256
- The result must fit within uint256

Caveats:
- This function does not work with fixed-point numbers_

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| x | uint256 | The multiplicand as an uint256 |
| offset | uint256 | The number of bit to shift x as an uint256 |
| denominator | uint256 | The divisor as an uint256 |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| result | uint256 | The result as an uint256 |

