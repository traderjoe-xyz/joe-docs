# BitMath
[Git Source](https://github.com/lfj-gg/joe-v2/blob/16f011d25e6bf6d0a0c479974345b623d491104f/src/libraries/math/BitMath.sol)

**Author:**
Trader Joe

Helper contract used for bit calculations


## Functions
### closestBitRight

*Returns the index of the closest bit on the right of x that is non null*


```solidity
function closestBitRight(uint256 x, uint8 bit) internal pure returns (uint256 id);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`x`|`uint256`|The value as a uint256|
|`bit`|`uint8`|The index of the bit to start searching at|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`id`|`uint256`|The index of the closest non null bit on the right of x. If there is no closest bit, it returns max(uint256)|


### closestBitLeft

*Returns the index of the closest bit on the left of x that is non null*


```solidity
function closestBitLeft(uint256 x, uint8 bit) internal pure returns (uint256 id);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`x`|`uint256`|The value as a uint256|
|`bit`|`uint8`|The index of the bit to start searching at|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`id`|`uint256`|The index of the closest non null bit on the left of x. If there is no closest bit, it returns max(uint256)|


### mostSignificantBit

*Returns the index of the most significant bit of x
This function returns 0 if x is 0*


```solidity
function mostSignificantBit(uint256 x) internal pure returns (uint8 msb);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`x`|`uint256`|The value as a uint256|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`msb`|`uint8`|The index of the most significant bit of x|


### leastSignificantBit

*Returns the index of the least significant bit of x
This function returns 255 if x is 0*


```solidity
function leastSignificantBit(uint256 x) internal pure returns (uint8 lsb);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`x`|`uint256`|The value as a uint256|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`lsb`|`uint8`|The index of the least significant bit of x|


