## Clone

Class with helper read functions for clone with immutable args.

### _getArgBytes

```solidity
function _getArgBytes(uint256 argOffset, uint256 length) internal pure returns (bytes memory arg)
```

Reads an immutable arg with type bytes

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| argOffset | uint256 | The offset of the arg in the immutable args |
| length | uint256 | The length of the arg |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| arg | bytes | The immutable bytes arg |

### _getArgAddress

```solidity
function _getArgAddress(uint256 argOffset) internal pure returns (address arg)
```

Reads an immutable arg with type address

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| argOffset | uint256 | The offset of the arg in the immutable args |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| arg | address | The immutable address arg |

### _getArgUint256

```solidity
function _getArgUint256(uint256 argOffset) internal pure returns (uint256 arg)
```

Reads an immutable arg with type uint256

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| argOffset | uint256 | The offset of the arg in the immutable args |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| arg | uint256 | The immutable uint256 arg |

### _getArgUint256Array

```solidity
function _getArgUint256Array(uint256 argOffset, uint256 length) internal pure returns (uint256[] memory arg)
```

Reads a uint256 array stored in the immutable args.

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| argOffset | uint256 | The offset of the arg in the immutable args |
| length | uint256 | The length of the arg |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| arg | uint256[] | The immutable uint256 array arg |

### _getArgUint64

```solidity
function _getArgUint64(uint256 argOffset) internal pure returns (uint64 arg)
```

Reads an immutable arg with type uint64

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| argOffset | uint256 | The offset of the arg in the immutable args |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| arg | uint64 | The immutable uint64 arg |

### _getArgUint16

```solidity
function _getArgUint16(uint256 argOffset) internal pure returns (uint16 arg)
```

Reads an immutable arg with type uint16

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| argOffset | uint256 | The offset of the arg in the immutable args |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| arg | uint16 | The immutable uint16 arg |

### _getArgUint8

```solidity
function _getArgUint8(uint256 argOffset) internal pure returns (uint8 arg)
```

Reads an immutable arg with type uint8

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| argOffset | uint256 | The offset of the arg in the immutable args |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| arg | uint8 | The immutable uint8 arg |

### _getImmutableArgsOffset

```solidity
function _getImmutableArgsOffset() internal pure returns (uint256 offset)
```

Reads the offset of the packed immutable args in calldata.

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| offset | uint256 | The offset of the packed immutable args in calldata. |