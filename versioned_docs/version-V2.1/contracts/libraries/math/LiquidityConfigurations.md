## Liquidity Configurations

This library contains functions to encode and decode the config of a pool and interact with the encoded bytes32.

### encodeParams

```solidity
function encodeParams(uint64 distributionX, uint64 distributionY, uint24 id) internal pure returns (bytes32 config)
```

Encode the distributionX, distributionY and id into a single bytes32

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| distributionX | uint64 | The distribution of the first token |
| distributionY | uint64 | The distribution of the second token |
| id | uint24 | The id of the pool |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| config | bytes32 | The encoded config as follows: [0 - 24[: id [24 - 88[: distributionY [88 - 152[: distributionX [152 - 256[: empty |

### decodeParams

```solidity
function decodeParams(bytes32 config) internal pure returns (uint64 distributionX, uint64 distributionY, uint24 id)
```

Decode the distributionX, distributionY and id from a single bytes32

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| config | bytes32 | The encoded config as follows: [0 - 24[: id [24 - 88[: distributionY [88 - 152[: distributionX [152 - 256[: empty |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| distributionX | uint64 | The distribution of the first token |
| distributionY | uint64 | The distribution of the second token |
| id | uint24 | The id of the bin to add the liquidity to |

### getAmountsAndId

```solidity
function getAmountsAndId(bytes32 config, bytes32 amountsIn) internal pure returns (bytes32, uint24)
```

Get the amounts and id from a config and amountsIn

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| config | bytes32 | The encoded config |
| amountsIn | bytes32 | The amounts to distribute as follows: [0 - 128[: x1 [128 - 256[: x2 |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| amounts | bytes32 | The distributed amounts as follows: [0 - 128[: x1 [128 - 256[: x2 |
| id | uint24 | The id of the bin to add the liquidity to |