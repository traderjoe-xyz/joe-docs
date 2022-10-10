---
sidebar_position: 0
sidebar_label: TreeMath
---

## TreeMath

Helper contract used for finding closest bin with liquidity

### findFirstBin

```solidity
function findFirstBin(mapping(uint256 => uint256)[3] _tree, uint24 _binId, bool _rightSide) internal view returns (uint24)
```

Returns the first id that is non zero, corresponding to a bin with
liquidity in it

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _tree | mapping(uint256 &#x3D;&gt; uint256)[3] | The storage slot of the tree |
| _binId | uint24 | the binId to start searching |
| _rightSide | bool | Whether we're searching in the right side of the tree (true) or the left side (false) for the closest non zero bit on the right or the left |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| [0] | uint24 | The closest non zero bit on the right (or left) side of the tree |

### addToTree

```solidity
function addToTree(mapping(uint256 => uint256)[3] _tree, uint256 _id) internal
```

### removeFromTree

```solidity
function removeFromTree(mapping(uint256 => uint256)[3] _tree, uint256 _id) internal
```

