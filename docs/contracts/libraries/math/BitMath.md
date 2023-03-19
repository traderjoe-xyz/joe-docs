## Bit Math

Helper contract used for bit calculations

### closestBitRight

```solidity
function closestBitRight(uint256 x, uint8 bit) internal pure returns (uint256 id)
```

Returns the index of the closest bit on the right of x that is non null

#### Parameters

| Name | Type    | Description                              |
| ---- | ------- | ---------------------------------------- |
| x    | uint256 | The value as a uint256                   |
| bit  | uint8   | The index of the bit to start searching at |

#### Return Values

| Name | Type    | Description                              |
| ---- | ------- | ---------------------------------------- |
| id   | uint256 | The index of the closest non null bit on the right of x. If there is no closest bit, it returns max(uint256) |

### closestBitLeft

```solidity
function closestBitLeft(uint256 x, uint8 bit) internal pure returns (uint256 id)
```

Returns the index of the closest bit on the left of x that is non null

#### Parameters

| Name | Type    | Description                              |
| ---- | ------- | ---------------------------------------- |
| x    | uint256 | The value as a uint256                   |
| bit  | uint8   | The index of the bit to start searching at |

#### Return Values

| Name | Type    | Description                              |
| ---- | ------- | ---------------------------------------- |
| id   | uint256 | The index of the closest non null bit on the left of x. If there is no closest bit, it returns max(uint256) |

### mostSignificantBit

```solidity
function mostSignificantBit(uint256 x) internal pure returns (uint8 msb)
```

Returns the index of the most significant bit of x. This function returns 0 if x is 0

#### Parameters

| Name | Type    | Description                              |
| ---- | ------- | ---------------------------------------- |
| x    | uint256 | The value as a uint256                   |

#### Return Values

| Name | Type  | Description                              |
| ---- | ----- | ---------------------------------------- |
| msb  | uint8 | The index of the most significant bit of x |

### leastSignificantBit

```solidity
function leastSignificantBit(uint256 x) internal pure returns (uint8 lsb)
```

Returns the index of the least significant bit of x. This function returns 255 if x is 0

#### Parameters

| Name | Type    | Description                              |
| ---- | ------- | ---------------------------------------- |
| x    | uint256 | The value as a uint256                   |

#### Return Values

| Name | Type  | Description                              |
| ---- | ----- | ---------------------------------------- |
| lsb  | uint8 | The index of the least significant bit of x |