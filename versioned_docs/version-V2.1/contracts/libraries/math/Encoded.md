## Encoded

Helper contract used for decoding bytes32 sample

### set

```solidity
function set(bytes32 encoded, uint256 value, uint256 mask, uint256 offset) internal pure returns (bytes32 newEncoded)
```

Internal function to set a value in an encoded bytes32 using a mask and offset

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| encoded | bytes32 | The previous encoded value |
| value | uint256 | The value to encode |
| mask | uint256 | The mask |
| offset | uint256 | The offset |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| newEncoded | bytes32 | The new encoded value |

### setBool

```solidity
function setBool(bytes32 encoded, bool boolean, uint256 offset) internal pure returns (bytes32 newEncoded)
```

Internal function to set a bool in an encoded bytes32 using an offset

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| encoded | bytes32 | The previous encoded value |
| boolean | bool | The bool to encode |
| offset | uint256 | The offset |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| newEncoded | bytes32 | The new encoded value |

### decode

```solidity
function decode(bytes32 encoded, uint256 mask, uint256 offset) internal pure returns (uint256 value)
```

Internal function to decode a bytes32 sample using a mask and offset

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| encoded | bytes32 | The encoded value |
| mask | uint256 | The mask |
| offset | uint256 | The offset |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| value | uint256 | The decoded value |

### decodeBool

```solidity
function decodeBool(bytes32 encoded, uint256 offset) internal pure returns (bool boolean)
```

Internal function to decode a bytes32 sample into a bool using an offset

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| encoded | bytes32 | The encoded value |
| offset | uint256 | The offset |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| boolean | bool | The decoded value as a bool |

### decodeUint8

```solidity
function decodeUint8(bytes32 encoded, uint256 offset) internal pure returns (uint8 value)
```

Internal function to decode a bytes32 sample into a uint8 using an offset

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| encoded | bytes32 | The encoded value |
| offset | uint256 | The offset |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| value | uint8 | The decoded value |

### decodeUint12

```solidity
function decodeUint12(bytes32 encoded, uint256 offset) internal pure returns (uint16 value)
```

Internal function to decode a bytes32 sample into a uint12 using an offset

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| encoded | bytes32 | The encoded value |
| offset | uint256 | The offset |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| value | uint16 | The decoded value as a uint16, since uint12 is not supported |

### decodeUint14

```solidity
function decodeUint14(bytes32 encoded, uint256 offset) internal pure returns (uint16 value)
```

Internal function to decode a bytes32 sample into a uint14 using an offset

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| encoded | bytes32 | The encoded value |
| offset | uint256 | The offset |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| value | uint16 | The decoded value as a uint16, since uint14 is not supported |

### decodeUint16

```solidity
function decodeUint16(bytes32 encoded, uint256 offset) internal pure returns (uint16 value)
```

Internal function to decode a bytes32 sample into a uint16 using an offset

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| encoded | bytes32 | The encoded value |
| offset | uint256 | The offset |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| value | uint16 | The decoded value |

### decodeUint20

```solidity
function decodeUint20(bytes32 encoded, uint256 offset) internal pure returns (uint24 value)
```

Internal function to decode a bytes32 sample into a uint20 using an offset

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| encoded | bytes32 | The encoded value |
| offset | uint256 | The offset |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| value | uint24 | The decoded value as a uint24, since uint20 is not supported |

### decodeUint24

```solidity
function decodeUint24(bytes32 encoded, uint256 offset) internal pure returns (uint24 value)
```

Internal function to decode a bytes32 sample into a uint24 using an offset

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| encoded | bytes32 | The encoded value |
| offset | uint256 | The offset |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| value | uint24 | The decoded value |

### decodeUint40

```solidity
function decodeUint40(bytes32 encoded, uint256 offset) internal pure returns (uint40 value)
```

Internal function to decode a bytes32 sample into a uint40 using an offset

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| encoded | bytes32 | The encoded value |
| offset | uint256 | The offset |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| value | uint40 | The decoded value |

### decodeUint64

```solidity
function decodeUint64(bytes32 encoded, uint256 offset) internal pure returns (uint64 value)
```

Internal function to decode a bytes32 sample into a uint64 using an offset

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| encoded | bytes32 | The encoded value |
| offset | uint256 | The offset |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| value | uint64 | The decoded value |

### decodeUint128

```solidity
function decodeUint128(bytes32 encoded, uint256 offset) internal pure returns (uint128 value)
```

Internal function to decode a bytes32 sample into a uint128 using an offset

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| encoded | bytes32 | The encoded value |
| offset | uint256 | The offset |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| value | uint128 | The decoded value |