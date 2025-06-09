# TreeMath
[Git Source](https://github.com/lfj-gg/joe-v2/blob/16f011d25e6bf6d0a0c479974345b623d491104f/src/libraries/math/TreeMath.sol)

**Author:**
Trader Joe

This library contains functions to interact with a tree of TreeUint24.


## Functions
### contains

*Returns true if the tree contains the id*


```solidity
function contains(TreeUint24 storage tree, uint24 id) internal view returns (bool);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`tree`|`TreeUint24`|The tree|
|`id`|`uint24`|The id|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bool`|True if the tree contains the id|


### add

*Adds the id to the tree and returns true if the id was not already in the tree
It will also propagate the change to the parent levels.*


```solidity
function add(TreeUint24 storage tree, uint24 id) internal returns (bool);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`tree`|`TreeUint24`|The tree|
|`id`|`uint24`|The id|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bool`|True if the id was not already in the tree|


### remove

*Removes the id from the tree and returns true if the id was in the tree.
It will also propagate the change to the parent levels.*


```solidity
function remove(TreeUint24 storage tree, uint24 id) internal returns (bool);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`tree`|`TreeUint24`|The tree|
|`id`|`uint24`|The id|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bool`|True if the id was in the tree|


### findFirstRight

*Returns the first id in the tree that is lower than or equal to the given id.
It will return type(uint24).max if there is no such id.*


```solidity
function findFirstRight(TreeUint24 storage tree, uint24 id) internal view returns (uint24);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`tree`|`TreeUint24`|The tree|
|`id`|`uint24`|The id|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint24`|The first id in the tree that is lower than or equal to the given id|


### findFirstLeft

*Returns the first id in the tree that is higher than or equal to the given id.
It will return 0 if there is no such id.*


```solidity
function findFirstLeft(TreeUint24 storage tree, uint24 id) internal view returns (uint24);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`tree`|`TreeUint24`|The tree|
|`id`|`uint24`|The id|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint24`|The first id in the tree that is higher than or equal to the given id|


### _closestBitRight

*Returns the first bit in the given leaves that is strictly lower than the given bit.
It will return type(uint256).max if there is no such bit.*


```solidity
function _closestBitRight(bytes32 leaves, uint8 bit) private pure returns (uint256);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`leaves`|`bytes32`|The leaves|
|`bit`|`uint8`|The bit|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint256`|The first bit in the given leaves that is strictly lower than the given bit|


### _closestBitLeft

*Returns the first bit in the given leaves that is strictly higher than the given bit.
It will return type(uint256).max if there is no such bit.*


```solidity
function _closestBitLeft(bytes32 leaves, uint8 bit) private pure returns (uint256);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`leaves`|`bytes32`|The leaves|
|`bit`|`uint8`|The bit|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint256`|The first bit in the given leaves that is strictly higher than the given bit|


## Structs
### TreeUint24

```solidity
struct TreeUint24 {
    bytes32 level0;
    mapping(bytes32 => bytes32) level1;
    mapping(bytes32 => bytes32) level2;
}
```

