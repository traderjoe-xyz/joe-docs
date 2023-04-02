## Tree Math

Liquidity Book Tree Math Library: This library contains functions to interact with a tree of TreeUint24.

### contains

```solidity
function contains(TreeUint24 storage tree, uint24 id) internal view returns (bool)
```

Returns true if the tree contains the id.

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| tree | TreeUint24 storage | The tree |
| id | uint24 | The id |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| none | bool | Returns true if the tree contains the id |

### add

```solidity
function add(TreeUint24 storage tree, uint24 id) internal returns (bool)
```

Adds the id to the tree and returns true if the id was not already in the tree. It will also propagate the change to the parent levels.

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| tree | TreeUint24 storage | The tree |
| id | uint24 | The id |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| none | bool | Returns true if the id was not already in the tree |

### remove

```solidity
function remove(TreeUint24 storage tree, uint24 id) internal returns (bool)
```

Removes the id from the tree and returns true if the id was in the tree. It will also propagate the change to the parent levels.

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| tree | TreeUint24 storage | The tree |
| id | uint24 | The id |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| none | bool |Returns true if the id was in the tree |

### findFirstRight

```solidity
function findFirstRight(TreeUint24 storage tree, uint24 id) internal view returns (uint24)
```

Returns the first id in the tree that is lower than or equal to the given id. It will return type(uint24).max if there is no such id.

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| tree | TreeUint24 storage | The tree |
| id | uint24 | The id |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| none | uint24 | Returns the first id in the tree that is lower than or equal to the given id |

### findFirstLeft

```solidity
function findFirstLeft(TreeUint24 storage tree, uint24 id) internal view returns (uint24)
```

Returns the first id in the tree that is higher than or equal to the given id. It will return 0 if there is no such id.

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| tree | TreeUint24 storage | The tree |
| id | uint24 | The id |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| none | uint24 | Returns the first id in the tree that is higher than or equal to the given id |

### findFirstLeft

```solidity
function findFirstLeft(TreeUint24 storage tree, uint24 id) internal view returns (uint24)
```

Returns the first id in the tree that is higher than or equal to the given id. It will return 0 if there is no such id.

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| tree | TreeUint24 storage | The tree |
| id | uint24 | The id |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
|  | uint24 | The first id in the tree that is higher than or equal to the given id |

### _closestBitRight

```solidity
function _closestBitRight(bytes32 leaves, uint8 bit) private pure returns (uint256)
```

Returns the first bit in the given leaves that is strictly lower than the given bit. It will return type(uint256).max if there is no such bit.

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| leaves | bytes32 | The leaves |
| bit | uint8 | The bit |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
|  | uint256 | The first bit in the given leaves that is strictly lower than the given bit |

### _closestBitLeft

```solidity
function _closestBitLeft(bytes32 leaves, uint8 bit) private pure returns (uint256)
```

Returns the first bit in the given leaves that is strictly higher than the given bit. It will return type(uint256).max if there is no such bit.

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| leaves | bytes32 | The leaves |
| bit | uint8 | The bit |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
|  | uint256 | The first bit in the given leaves that is strictly higher than the given bit |