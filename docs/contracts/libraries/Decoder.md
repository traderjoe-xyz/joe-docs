---
sidebar_position: 0
sidebar_label: Decoder
---

## Decoder

Helper contract used for decoding bytes32 sample

### decode

```solidity
function decode(bytes32 _sample, uint256 _mask, uint256 _offset) internal pure returns (uint256 value)
```

Internal function to decode a bytes32 sample using a mask and offset

_This function can overflow_

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _sample | bytes32 | The sample as a bytes32 |
| _mask | uint256 | The mask |
| _offset | uint256 | The offset |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| value | uint256 | The decoded value |

