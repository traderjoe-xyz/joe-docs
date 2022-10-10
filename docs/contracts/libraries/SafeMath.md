---
sidebar_position: 0
sidebar_label: SafeMath
---

## SafeMath

Helper contract used for calculating absolute value safely

### absSub

```solidity
function absSub(uint256 x, uint256 y) internal pure returns (uint256)
```

absSub, can't underflow or overflow

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| x | uint256 | The first value |
| y | uint256 | The second value |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| [0] | uint256 | The result of x - y |

