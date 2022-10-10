---
sidebar_position: 0
sidebar_label: 
---

## BitMath

Helper contract used for bit calculations

### closestBit

```solidity
function closestBit(uint256 _integer, uint8 _bit, bool _rightSide) internal pure returns (uint256)
```

Returns the closest non-zero bit of `integer` to the right (of left) of the `bit` bits that is not `bit`

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _integer | uint256 | The integer as a uint256 |
| _bit | uint8 | The bit index |
| _rightSide | bool | Whether we're searching in the right side of the tree (true) or the left side (false) |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| [0] | uint256 | The index of the closest non-zero bit. If there is no closest bit, it returns max(uint256) |

### significantBit

```solidity
function significantBit(uint256 _integer, bool _isMostSignificant) internal pure returns (uint8)
```

Returns the most (or least) significant bit of `_integer`

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _integer | uint256 | The integer |
| _isMostSignificant | bool | Whether we want the most (true) or the least (false) significant bit |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| [0] | uint8 | The index of the most (or least) significant bit |

### closestBitRight

```solidity
function closestBitRight(uint256 x, uint8 bit) internal pure returns (uint256 id)
```

Returns the index of the closest bit on the right of x that is non null

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| x | uint256 | The value as a uint256 |
| bit | uint8 | The index of the bit to start searching at |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| id | uint256 | The index of the closest non null bit on the right of x. If there is no closest bit, it returns max(uint256) |

### closestBitLeft

```solidity
function closestBitLeft(uint256 x, uint8 bit) internal pure returns (uint256 id)
```

Returns the index of the closest bit on the left of x that is non null

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| x | uint256 | The value as a uint256 |
| bit | uint8 | The index of the bit to start searching at |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| id | uint256 | The index of the closest non null bit on the left of x. If there is no closest bit, it returns max(uint256) |

### mostSignificantBit

```solidity
function mostSignificantBit(uint256 x) internal pure returns (uint8 msb)
```

Returns the index of the most significant bit of x

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| x | uint256 | The value as a uint256 |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| msb | uint8 | The index of the most significant bit of x |

### leastSignificantBit

```solidity
function leastSignificantBit(uint256 x) internal pure returns (uint8 lsb)
```

Returns the index of the least significant bit of x

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| x | uint256 | The value as a uint256 |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| lsb | uint8 | The index of the least significant bit of x |

