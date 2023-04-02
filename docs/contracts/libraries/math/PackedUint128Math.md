## Packed Uint128 Math

This library contains functions to encode and decode two uint128 into a single bytes32 and interact with the encoded bytes32.

### encode

```solidity
function encode(uint128 x1, uint128 x2) internal pure returns (bytes32 z)
```

Encodes two uint128 into a single bytes32.

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| x1 | uint128 | The first uint128 |
| x2 | uint128 | The second uint128 |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| z | bytes32 | The encoded bytes32 as follows:<br/>[0 - 128[: x1<br/>[128 - 256[: x2|

### encodeFirst

```solidity
function encodeFirst(uint128 x1) internal pure returns (bytes32 z)
```

Encodes a uint128 into a single bytes32 as the first uint128.

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| x1 | uint128 | The uint128 |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| z | bytes32 | The encoded bytes32 as follows:<br/>[0 - 128[: x1<br/>[128 - 256[: empty|

### encodeSecond

```solidity
function encodeSecond(uint128 x2) internal pure returns (bytes32 z)
```

Encodes a uint128 into a single bytes32 as the second uint128.

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| x2 | uint128 | The uint128 |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| z | bytes32 | The encoded bytes32 as follows:<br/>[0 - 128[: empty<br/>[128 - 256[: x2|

### encode

```solidity
function encode(uint128 x, bool first) internal pure returns (bytes32 z)
```

Encodes a uint128 into a single bytes32 as the first or second uint128.

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| x | uint128 | The uint128 |
| first | bool | Whether to encode as the first or second uint128 |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| z | bytes32 | The encoded bytes32 as follows:<br/>if first:<br/>[0 - 128[: x<br/>[128 - 256[: empty<br/>else:<br/>[0 - 128[: empty<br/>[128 - 256[: x|

### decode

```solidity
function decode(bytes32 z) internal pure returns (uint128 x1, uint128 x2)
```

Decodes a bytes32 into two uint128.

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| z | bytes32 | The encoded bytes32 as follows:<br/>[0 - 128[: x1<br/>[128 - 256[: x2|

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| x1 | uint128 | The first uint128 |
| x2 | uint128 | The second uint128 |

### decodeX

```solidity
function decodeX(bytes32 z) internal pure returns (uint128 x1)
```

Decodes a bytes32 into a uint128 as the first uint128.

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| z | bytes32 | The encoded bytes32 as follows:<br/>[0 - 128[: x1<br/>[128 - 256[: any|

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| x1 | uint128 | The first uint128 |

### decodeY

```solidity
function decodeY(bytes32 z) internal pure returns (uint128 x2)
```

Decodes a bytes32 into a uint128 as the second uint128.

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| z | bytes32 | The encoded bytes32 as follows: [0 - 128[: any; [128 - 256[: x2 |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| x2 | uint128 | The second uint128 |

### decode

```solidity
function decode(bytes32 z, bool first) internal pure returns (uint128 x)
```

Decodes a bytes32 into a uint128 as the first or second uint128.

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| z | bytes32 | The encoded bytes32 as follows: if first: [0 - 128[: x1; [128 - 256[: empty; else: [0 - 128[: empty; [128 - 256[: x2 |
| first | bool | Whether to decode as the first or second uint128 |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| x | uint128 | The decoded uint128 |

### add

```solidity
function add(bytes32 x, bytes32 y) internal pure returns (bytes32 z)
```

Adds two encoded bytes32, reverting on overflow on any of the uint128.

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| x | bytes32 | The first bytes32 encoded as follows: [0 - 128[: x1; [128 - 256[: x2 |
| y | bytes32 | The second bytes32 encoded as follows: [0 - 128[: y1; [128 - 256[: y2 |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| z | bytes32 | The sum of x and y encoded as follows: [0 - 128[: x1 + y1; [128 - 256[: x2 + y2 |

### add

```solidity
function add(bytes32 x, uint128 y1, uint128 y2) internal pure returns (bytes32)
```

Adds an encoded bytes32 and two uint128, reverting on overflow on any of the uint128.

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| x | bytes32 | The bytes32 encoded as follows: [0 - 128[: x1; [128 - 256[: x2 |
| y1 | uint128 | The first uint128 |
| y2 | uint128 | The second uint128 |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
|  | bytes32 | The sum of x and y encoded as follows: [0 - 128[: x1 + y1; [128 - 256[: x2 + y2 |

### sub

```solidity
function sub(bytes32 x, bytes32 y) internal pure returns (bytes32 z)
```

Subtracts two encoded bytes32, reverting on underflow on any of the uint128.

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| x | bytes32 | The first bytes32 encoded as follows: [0 - 128[: x1; [128 - 256[: x2 |
| y | bytes32 | The second bytes32 encoded as follows: [0 - 128[: y1; [128 - 256[: y2 |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| z | bytes32 | The difference of x and y encoded as follows: [0 - 128[: x1 - y1; [128 - 256[: x2 - y2 |

### sub

```solidity
function sub(bytes32 x, uint128 y1, uint128 y2) internal pure returns (bytes32)
```

Subtracts an encoded bytes32 and two uint128, reverting on underflow on any of the uint128.

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| x | bytes32 | The bytes32 encoded as follows: [0 - 128[: x1; [128 - 256[: x2 |
| y1 | uint128 | The first uint128 |
| y2 | uint128 | The second uint128 |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
|  | bytes32 | The difference of x and y encoded as follows: [0 - 128[: x1 - y1; [128 - 256[: x2 - y2 |

### lt

```solidity
function lt(bytes32 x, bytes32 y) internal pure returns (bool)
```

Returns whether any of the uint128 of x is greater than the corresponding uint128 of y.

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| x | bytes32 | The first bytes32 encoded as follows: [0 - 128[: x1; [128 - 256[: x2 |
| y | bytes32 | The second bytes32 encoded as follows: [0 - 128[: y1; [128 - 256[: y2 |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
|  | bool | x1 < y1 or x2 < y2 |

### gt

```solidity
function gt(bytes32 x, bytes32 y) internal pure returns (bool)
```

Returns whether any of the uint128 of x is greater than or equal to the corresponding uint128 of y.

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| x | bytes32 | The first bytes32 encoded as follows: [0 - 128[: x1; [128 - 256[: x2 |
| y | bytes32 | The second bytes32 encoded as follows: [0 - 128[: y1; [128 - 256[: y2 |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
|  | bool | x1 > y1 or x2 > y2 |

### scalarMulShiftRoundUp

```solidity
function scalarMulShiftRoundUp(bytes32 x, uint256 multiplier) internal pure returns (bytes32 z)
```

Multiplies an encoded bytes32 by a uint256 then shifts the result 128 bits to the right, rounding up.

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| x | bytes32 | The bytes32 encoded as follows: [0 - 128[: x1 [128 - 256[: x2 |
| multiplier | uint256 | The uint128 to multiply by |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| z | bytes32 | The product of x and multiplier encoded as follows: [0 - 128[: ceil((x1 * multiplier) / 2^128) [128 - 256[: ceil((x2 * multiplier) / 2^128) |

### scalarMulDivBasisPointRoundDown

```solidity
function scalarMulDivBasisPointRoundDown(bytes32 x, uint128 multiplier) internal pure returns (bytes32 z)
```

Multiplies an encoded bytes32 by a uint128 then divides the result by 10_000, rounding down. The result can't overflow as the multiplier needs to be smaller or equal to 10_000.

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| x | bytes32 | The bytes32 encoded as follows: [0 - 128[: x1 [128 - 256[: x2 |
| multiplier | uint128 | The uint128 to multiply by (must be smaller or equal to 10_000) |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| z | bytes32 | The product of x and multiplier encoded as follows: [0 - 128[: floor((x1 * multiplier) / 10_000) [128 - 256[: floor((x2 * multiplier) / 10_000) |