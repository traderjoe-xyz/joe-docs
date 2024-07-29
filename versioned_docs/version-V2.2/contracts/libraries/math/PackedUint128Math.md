# PackedUint128Math
[Git Source](https://github.com/traderjoe-xyz/joe-v2/blob/16f011d25e6bf6d0a0c479974345b623d491104f/src/libraries/math/PackedUint128Math.sol)

**Author:**
Trader Joe

This library contains functions to encode and decode two uint128 into a single bytes32
and interact with the encoded bytes32.


## State Variables
### OFFSET

```solidity
uint256 private constant OFFSET = 128;
```


### MASK_128

```solidity
uint256 private constant MASK_128 = 0xffffffffffffffffffffffffffffffff;
```


### MASK_128_PLUS_ONE

```solidity
uint256 private constant MASK_128_PLUS_ONE = MASK_128 + 1;
```


## Functions
### encode

*Encodes two uint128 into a single bytes32*


```solidity
function encode(uint128 x1, uint128 x2) internal pure returns (bytes32 z);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`x1`|`uint128`|The first uint128|
|`x2`|`uint128`|The second uint128|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`z`|`bytes32`|The encoded bytes32 as follows: [0 - 128[: x1 [128 - 256[: x2|


### encodeFirst

*Encodes a uint128 into a single bytes32 as the first uint128*


```solidity
function encodeFirst(uint128 x1) internal pure returns (bytes32 z);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`x1`|`uint128`|The uint128|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`z`|`bytes32`|The encoded bytes32 as follows: [0 - 128[: x1 [128 - 256[: empty|


### encodeSecond

*Encodes a uint128 into a single bytes32 as the second uint128*


```solidity
function encodeSecond(uint128 x2) internal pure returns (bytes32 z);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`x2`|`uint128`|The uint128|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`z`|`bytes32`|The encoded bytes32 as follows: [0 - 128[: empty [128 - 256[: x2|


### encode

*Encodes a uint128 into a single bytes32 as the first or second uint128*


```solidity
function encode(uint128 x, bool first) internal pure returns (bytes32 z);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`x`|`uint128`|The uint128|
|`first`|`bool`|Whether to encode as the first or second uint128|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`z`|`bytes32`|The encoded bytes32 as follows: if first: [0 - 128[: x [128 - 256[: empty else: [0 - 128[: empty [128 - 256[: x|


### decode

*Decodes a bytes32 into two uint128*


```solidity
function decode(bytes32 z) internal pure returns (uint128 x1, uint128 x2);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`z`|`bytes32`|The encoded bytes32 as follows: [0 - 128[: x1 [128 - 256[: x2|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`x1`|`uint128`|The first uint128|
|`x2`|`uint128`|The second uint128|


### decodeX

*Decodes a bytes32 into a uint128 as the first uint128*


```solidity
function decodeX(bytes32 z) internal pure returns (uint128 x);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`z`|`bytes32`|The encoded bytes32 as follows: [0 - 128[: x [128 - 256[: any|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`x`|`uint128`|The first uint128|


### decodeY

*Decodes a bytes32 into a uint128 as the second uint128*


```solidity
function decodeY(bytes32 z) internal pure returns (uint128 y);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`z`|`bytes32`|The encoded bytes32 as follows: [0 - 128[: any [128 - 256[: y|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`y`|`uint128`|The second uint128|


### decode

*Decodes a bytes32 into a uint128 as the first or second uint128*


```solidity
function decode(bytes32 z, bool first) internal pure returns (uint128 x);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`z`|`bytes32`|The encoded bytes32 as follows: if first: [0 - 128[: x1 [128 - 256[: empty else: [0 - 128[: empty [128 - 256[: x2|
|`first`|`bool`|Whether to decode as the first or second uint128|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`x`|`uint128`|The decoded uint128|


### add

*Adds two encoded bytes32, reverting on overflow on any of the uint128*


```solidity
function add(bytes32 x, bytes32 y) internal pure returns (bytes32 z);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`x`|`bytes32`|The first bytes32 encoded as follows: [0 - 128[: x1 [128 - 256[: x2|
|`y`|`bytes32`|The second bytes32 encoded as follows: [0 - 128[: y1 [128 - 256[: y2|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`z`|`bytes32`|The sum of x and y encoded as follows: [0 - 128[: x1 + y1 [128 - 256[: x2 + y2|


### add

*Adds an encoded bytes32 and two uint128, reverting on overflow on any of the uint128*


```solidity
function add(bytes32 x, uint128 y1, uint128 y2) internal pure returns (bytes32);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`x`|`bytes32`|The bytes32 encoded as follows: [0 - 128[: x1 [128 - 256[: x2|
|`y1`|`uint128`|The first uint128|
|`y2`|`uint128`|The second uint128|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bytes32`|z The sum of x and y encoded as follows: [0 - 128[: x1 + y1 [128 - 256[: x2 + y2|


### sub

*Subtracts two encoded bytes32, reverting on underflow on any of the uint128*


```solidity
function sub(bytes32 x, bytes32 y) internal pure returns (bytes32 z);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`x`|`bytes32`|The first bytes32 encoded as follows: [0 - 128[: x1 [128 - 256[: x2|
|`y`|`bytes32`|The second bytes32 encoded as follows: [0 - 128[: y1 [128 - 256[: y2|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`z`|`bytes32`|The difference of x and y encoded as follows: [0 - 128[: x1 - y1 [128 - 256[: x2 - y2|


### sub

*Subtracts an encoded bytes32 and two uint128, reverting on underflow on any of the uint128*


```solidity
function sub(bytes32 x, uint128 y1, uint128 y2) internal pure returns (bytes32);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`x`|`bytes32`|The bytes32 encoded as follows: [0 - 128[: x1 [128 - 256[: x2|
|`y1`|`uint128`|The first uint128|
|`y2`|`uint128`|The second uint128|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bytes32`|z The difference of x and y encoded as follows: [0 - 128[: x1 - y1 [128 - 256[: x2 - y2|


### lt

*Returns whether any of the uint128 of x is strictly greater than the corresponding uint128 of y*


```solidity
function lt(bytes32 x, bytes32 y) internal pure returns (bool);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`x`|`bytes32`|The first bytes32 encoded as follows: [0 - 128[: x1 [128 - 256[: x2|
|`y`|`bytes32`|The second bytes32 encoded as follows: [0 - 128[: y1 [128 - 256[: y2|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bool`|x1 < y1 || x2 < y2|


### gt

*Returns whether any of the uint128 of x is strictly greater than the corresponding uint128 of y*


```solidity
function gt(bytes32 x, bytes32 y) internal pure returns (bool);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`x`|`bytes32`|The first bytes32 encoded as follows: [0 - 128[: x1 [128 - 256[: x2|
|`y`|`bytes32`|The second bytes32 encoded as follows: [0 - 128[: y1 [128 - 256[: y2|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bool`|x1 < y1 || x2 < y2|


### scalarMulDivBasisPointRoundDown

*Multiplies an encoded bytes32 by a uint128 then divides the result by 10_000, rounding down
The result can't overflow as the multiplier needs to be smaller or equal to 10_000*


```solidity
function scalarMulDivBasisPointRoundDown(bytes32 x, uint128 multiplier) internal pure returns (bytes32 z);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`x`|`bytes32`|The bytes32 encoded as follows: [0 - 128[: x1 [128 - 256[: x2|
|`multiplier`|`uint128`|The uint128 to multiply by (must be smaller or equal to 10_000)|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`z`|`bytes32`|The product of x and multiplier encoded as follows: [0 - 128[: floor((x1 * multiplier) / 10_000) [128 - 256[: floor((x2 * multiplier) / 10_000)|


## Errors
### PackedUint128Math__AddOverflow

```solidity
error PackedUint128Math__AddOverflow();
```

### PackedUint128Math__SubUnderflow

```solidity
error PackedUint128Math__SubUnderflow();
```

### PackedUint128Math__MultiplierTooLarge

```solidity
error PackedUint128Math__MultiplierTooLarge();
```

