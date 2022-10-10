---
sidebar_position: 0
sidebar_label: Samples
---

## Samples

Helper contract used for oracle samples operations

### update

```solidity
function update(bytes32 _lastSample, uint256 _activeId, uint256 _volatilityAccumulated, uint256 _binCrossed) internal view returns (bytes32 packedSample)
```

Function to update a sample

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _lastSample | bytes32 | The latest sample of the oracle |
| _activeId | uint256 | The active index of the pair during the latest swap |
| _volatilityAccumulated | uint256 | The volatility accumulated of the pair during the latest swap |
| _binCrossed | uint256 | The bin crossed during the latest swap |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| packedSample | bytes32 | The packed sample as bytes32 |

### pack

```solidity
function pack(uint256 _cumulativeBinCrossed, uint256 _cumulativeVolatilityAccumulated, uint256 _cumulativeId, uint256 _timestamp, uint256 _initialized) internal pure returns (bytes32 packedSample)
```

Function to pack cumulative values

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _cumulativeBinCrossed | uint256 | The cumulative bin crossed |
| _cumulativeVolatilityAccumulated | uint256 | The cumulative volatility accumulated |
| _cumulativeId | uint256 | The cumulative index |
| _timestamp | uint256 | The timestamp |
| _initialized | uint256 | The initialized value |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| packedSample | bytes32 | The packed sample as bytes32 |

### initialized

```solidity
function initialized(bytes32 _packedSample) internal pure returns (uint256)
```

View function to return the initialized value

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _packedSample | bytes32 | The packed sample |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| [0] | uint256 | The initialized value |

### timestamp

```solidity
function timestamp(bytes32 _packedSample) internal pure returns (uint256)
```

View function to return the timestamp value

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _packedSample | bytes32 | The packed sample |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| [0] | uint256 | The timestamp value |

### cumulativeId

```solidity
function cumulativeId(bytes32 _packedSample) internal pure returns (uint256)
```

View function to return the cumulative id value

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _packedSample | bytes32 | The packed sample |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| [0] | uint256 | The cumulative id value |

### cumulativeVolatilityAccumulated

```solidity
function cumulativeVolatilityAccumulated(bytes32 _packedSample) internal pure returns (uint256)
```

View function to return the cumulative volatility accumulated value

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _packedSample | bytes32 | The packed sample |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| [0] | uint256 | The cumulative volatility accumulated value |

### cumulativeBinCrossed

```solidity
function cumulativeBinCrossed(bytes32 _packedSample) internal pure returns (uint256)
```

View function to return the cumulative bin crossed value

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _packedSample | bytes32 | The packed sample |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| [0] | uint256 | The cumulative bin crossed value |

