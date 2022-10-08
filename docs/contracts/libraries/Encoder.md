---
sidebar_label: Encoder
---

### encode

```solidity
function encode(uint256 _value, uint256 _mask, uint256 _offset) internal pure returns (bytes32 sample)
```

Internal function to encode a uint256 value using a mask and offset

_This function can underflow_

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _value | uint256 | The value as a uint256 |
| _mask | uint256 | The mask |
| _offset | uint256 | The offset |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| sample | bytes32 | The encoded bytes32 sample |

