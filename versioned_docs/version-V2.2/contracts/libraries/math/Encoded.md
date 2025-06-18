# Encoded
[Git Source](https://github.com/lfj-gg/joe-v2/blob/16f011d25e6bf6d0a0c479974345b623d491104f/src/libraries/math/Encoded.sol)

**Author:**
Trader Joe

Helper contract used for decoding bytes32 sample


## State Variables
### MASK_UINT1

```solidity
uint256 internal constant MASK_UINT1 = 0x1;
```


### MASK_UINT8

```solidity
uint256 internal constant MASK_UINT8 = 0xff;
```


### MASK_UINT12

```solidity
uint256 internal constant MASK_UINT12 = 0xfff;
```


### MASK_UINT14

```solidity
uint256 internal constant MASK_UINT14 = 0x3fff;
```


### MASK_UINT16

```solidity
uint256 internal constant MASK_UINT16 = 0xffff;
```


### MASK_UINT20

```solidity
uint256 internal constant MASK_UINT20 = 0xfffff;
```


### MASK_UINT24

```solidity
uint256 internal constant MASK_UINT24 = 0xffffff;
```


### MASK_UINT40

```solidity
uint256 internal constant MASK_UINT40 = 0xffffffffff;
```


### MASK_UINT64

```solidity
uint256 internal constant MASK_UINT64 = 0xffffffffffffffff;
```


### MASK_UINT128

```solidity
uint256 internal constant MASK_UINT128 = 0xffffffffffffffffffffffffffffffff;
```


## Functions
### set

Internal function to set a value in an encoded bytes32 using a mask and offset

*This function can overflow*


```solidity
function set(bytes32 encoded, uint256 value, uint256 mask, uint256 offset) internal pure returns (bytes32 newEncoded);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`encoded`|`bytes32`|The previous encoded value|
|`value`|`uint256`|The value to encode|
|`mask`|`uint256`|The mask|
|`offset`|`uint256`|The offset|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`newEncoded`|`bytes32`|The new encoded value|


### setBool

Internal function to set a bool in an encoded bytes32 using an offset

*This function can overflow*


```solidity
function setBool(bytes32 encoded, bool boolean, uint256 offset) internal pure returns (bytes32 newEncoded);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`encoded`|`bytes32`|The previous encoded value|
|`boolean`|`bool`|The bool to encode|
|`offset`|`uint256`|The offset|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`newEncoded`|`bytes32`|The new encoded value|


### decode

Internal function to decode a bytes32 sample using a mask and offset

*This function can overflow*


```solidity
function decode(bytes32 encoded, uint256 mask, uint256 offset) internal pure returns (uint256 value);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`encoded`|`bytes32`|The encoded value|
|`mask`|`uint256`|The mask|
|`offset`|`uint256`|The offset|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`value`|`uint256`|The decoded value|


### decodeBool

Internal function to decode a bytes32 sample into a bool using an offset

*This function can overflow*


```solidity
function decodeBool(bytes32 encoded, uint256 offset) internal pure returns (bool boolean);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`encoded`|`bytes32`|The encoded value|
|`offset`|`uint256`|The offset|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`boolean`|`bool`|The decoded value as a bool|


### decodeUint8

Internal function to decode a bytes32 sample into a uint8 using an offset

*This function can overflow*


```solidity
function decodeUint8(bytes32 encoded, uint256 offset) internal pure returns (uint8 value);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`encoded`|`bytes32`|The encoded value|
|`offset`|`uint256`|The offset|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`value`|`uint8`|The decoded value|


### decodeUint12

Internal function to decode a bytes32 sample into a uint12 using an offset

*This function can overflow*


```solidity
function decodeUint12(bytes32 encoded, uint256 offset) internal pure returns (uint16 value);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`encoded`|`bytes32`|The encoded value|
|`offset`|`uint256`|The offset|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`value`|`uint16`|The decoded value as a uint16, since uint12 is not supported|


### decodeUint14

Internal function to decode a bytes32 sample into a uint14 using an offset

*This function can overflow*


```solidity
function decodeUint14(bytes32 encoded, uint256 offset) internal pure returns (uint16 value);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`encoded`|`bytes32`|The encoded value|
|`offset`|`uint256`|The offset|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`value`|`uint16`|The decoded value as a uint16, since uint14 is not supported|


### decodeUint16

Internal function to decode a bytes32 sample into a uint16 using an offset

*This function can overflow*


```solidity
function decodeUint16(bytes32 encoded, uint256 offset) internal pure returns (uint16 value);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`encoded`|`bytes32`|The encoded value|
|`offset`|`uint256`|The offset|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`value`|`uint16`|The decoded value|


### decodeUint20

Internal function to decode a bytes32 sample into a uint20 using an offset

*This function can overflow*


```solidity
function decodeUint20(bytes32 encoded, uint256 offset) internal pure returns (uint24 value);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`encoded`|`bytes32`|The encoded value|
|`offset`|`uint256`|The offset|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`value`|`uint24`|The decoded value as a uint24, since uint20 is not supported|


### decodeUint24

Internal function to decode a bytes32 sample into a uint24 using an offset

*This function can overflow*


```solidity
function decodeUint24(bytes32 encoded, uint256 offset) internal pure returns (uint24 value);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`encoded`|`bytes32`|The encoded value|
|`offset`|`uint256`|The offset|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`value`|`uint24`|The decoded value|


### decodeUint40

Internal function to decode a bytes32 sample into a uint40 using an offset

*This function can overflow*


```solidity
function decodeUint40(bytes32 encoded, uint256 offset) internal pure returns (uint40 value);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`encoded`|`bytes32`|The encoded value|
|`offset`|`uint256`|The offset|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`value`|`uint40`|The decoded value|


### decodeUint64

Internal function to decode a bytes32 sample into a uint64 using an offset

*This function can overflow*


```solidity
function decodeUint64(bytes32 encoded, uint256 offset) internal pure returns (uint64 value);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`encoded`|`bytes32`|The encoded value|
|`offset`|`uint256`|The offset|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`value`|`uint64`|The decoded value|


### decodeUint128

Internal function to decode a bytes32 sample into a uint128 using an offset

*This function can overflow*


```solidity
function decodeUint128(bytes32 encoded, uint256 offset) internal pure returns (uint128 value);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`encoded`|`bytes32`|The encoded value|
|`offset`|`uint256`|The offset|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`value`|`uint128`|The decoded value|


