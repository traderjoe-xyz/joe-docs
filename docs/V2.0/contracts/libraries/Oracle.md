---
sidebar_position: 0
sidebar_label: Oracle
---

## Oracle

Helper contract for oracle

### Sample

```solidity
struct Sample {
  uint256 timestamp;
  uint256 cumulativeId;
  uint256 cumulativeVolatilityAccumulated;
  uint256 cumulativeBinCrossed;
}
```

### getSampleAt

```solidity
function getSampleAt(bytes32[65535] _oracle, uint256 _activeSize, uint256 _activeId, uint256 _lookUpTimestamp) internal view returns (uint256 timestamp, uint256 cumulativeId, uint256 cumulativeVolatilityAccumulated, uint256 cumulativeBinCrossed)
```

View function to get the oracle's sample at `_ago` seconds

_Return a linearized sample, the weighted average of 2 neighboring samples_

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _oracle | bytes32[65535] | The oracle storage pointer |
| _activeSize | uint256 | The size of the oracle (without empty data) |
| _activeId | uint256 | The active index of the oracle |
| _lookUpTimestamp | uint256 | The looked up date |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| timestamp | uint256 | The timestamp of the sample |
| cumulativeId | uint256 | The weighted average cumulative id |
| cumulativeVolatilityAccumulated | uint256 | The weighted average cumulative volatility accumulated |
| cumulativeBinCrossed | uint256 | The weighted average cumulative bin crossed |

### update

```solidity
function update(bytes32[65535] _oracle, uint256 _size, uint256 _sampleLifetime, uint256 _lastTimestamp, uint256 _lastIndex, uint256 _activeId, uint256 _volatilityAccumulated, uint256 _binCrossed) internal returns (uint256 updatedIndex)
```

Function to update a sample

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _oracle | bytes32[65535] | The oracle storage pointer |
| _size | uint256 | The size of the oracle (last ids can be empty) |
| _sampleLifetime | uint256 | The lifetime of a sample, it accumulates information for up to this timestamp |
| _lastTimestamp | uint256 | The timestamp of the creation of the oracle's latest sample |
| _lastIndex | uint256 | The index of the oracle's latest sample |
| _activeId | uint256 | The active index of the pair during the latest swap |
| _volatilityAccumulated | uint256 | The volatility accumulated of the pair during the latest swap |
| _binCrossed | uint256 | The bin crossed during the latest swap |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| updatedIndex | uint256 | The oracle updated index, it is either the same as before, or the next one |

### initialize

```solidity
function initialize(bytes32[65535] _oracle, uint256 _index) internal
```

Initialize the sample

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _oracle | bytes32[65535] | The oracle storage pointer |
| _index | uint256 | The index to initialize |
