# Clone
[Git Source](https://github.com/traderjoe-xyz/joe-v2/blob/16f011d25e6bf6d0a0c479974345b623d491104f/src/libraries/Clone.sol)

**Authors:**
Trader Joe, Solady (https://github.com/vectorized/solady/blob/main/src/utils/Clone.sol), Adapted from clones with immutable args by zefram.eth, Saw-mon & Natalie
(https://github.com/Saw-mon-and-Natalie/clones-with-immutable-args)

Class with helper read functions for clone with immutable args.


## Functions
### _getArgBytes

*Reads an immutable arg with type bytes*


```solidity
function _getArgBytes(uint256 argOffset, uint256 length) internal pure returns (bytes memory arg);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`argOffset`|`uint256`|The offset of the arg in the immutable args|
|`length`|`uint256`|The length of the arg|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`arg`|`bytes`|The immutable bytes arg|


### _getArgAddress

*Reads an immutable arg with type address*


```solidity
function _getArgAddress(uint256 argOffset) internal pure returns (address arg);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`argOffset`|`uint256`|The offset of the arg in the immutable args|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`arg`|`address`|The immutable address arg|


### _getArgUint256

*Reads an immutable arg with type uint256*


```solidity
function _getArgUint256(uint256 argOffset) internal pure returns (uint256 arg);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`argOffset`|`uint256`|The offset of the arg in the immutable args|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`arg`|`uint256`|The immutable uint256 arg|


### _getArgUint256Array

*Reads a uint256 array stored in the immutable args.*


```solidity
function _getArgUint256Array(uint256 argOffset, uint256 length) internal pure returns (uint256[] memory arg);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`argOffset`|`uint256`|The offset of the arg in the immutable args|
|`length`|`uint256`|The length of the arg|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`arg`|`uint256[]`|The immutable uint256 array arg|


### _getArgUint64

*Reads an immutable arg with type uint64*


```solidity
function _getArgUint64(uint256 argOffset) internal pure returns (uint64 arg);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`argOffset`|`uint256`|The offset of the arg in the immutable args|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`arg`|`uint64`|The immutable uint64 arg|


### _getArgUint16

*Reads an immutable arg with type uint16*


```solidity
function _getArgUint16(uint256 argOffset) internal pure returns (uint16 arg);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`argOffset`|`uint256`|The offset of the arg in the immutable args|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`arg`|`uint16`|The immutable uint16 arg|


### _getArgUint8

*Reads an immutable arg with type uint8*


```solidity
function _getArgUint8(uint256 argOffset) internal pure returns (uint8 arg);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`argOffset`|`uint256`|The offset of the arg in the immutable args|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`arg`|`uint8`|The immutable uint8 arg|


### _getImmutableArgsOffset

*Reads the offset of the packed immutable args in calldata.*


```solidity
function _getImmutableArgsOffset() internal pure returns (uint256 offset);
```
**Returns**

|Name|Type|Description|
|----|----|-----------|
|`offset`|`uint256`|The offset of the packed immutable args in calldata.|


