## Oracle Helper

This library contains functions to manage the oracle. The oracle samples are stored in a single bytes32 array. Each sample is encoded as follows: <br/>

0 - 16: oracle length (16 bits)<br/>
16 - 80: cumulative id (64 bits)<br/>
80 - 144: cumulative volatility accumulator (64 bits)<br/>
144 - 208: cumulative bin crossed (64 bits)<br/>
208 - 216: sample lifetime (8 bits)<br/>
216 - 256: sample creation timestamp (40 bits)<br/>

### getSample

```solidity
function getSample(Oracle storage oracle, uint16 oracleId) internal view checkOracleId(oracleId) returns (bytes32 sample)
```

Returns the sample at the given oracleId

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| oracle | Oracle storage | The oracle |
| oracleId | uint16 | The oracle id |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| sample | bytes32 | The sample |

### getActiveSampleAndSize

```solidity
function getActiveSampleAndSize(Oracle storage oracle, uint16 oracleId) internal view returns (bytes32 activeSample, uint16 activeSize)
```

Returns the active sample and the active size of the oracle

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| oracle | Oracle storage | The oracle |
| oracleId | uint16 | The oracle id |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| activeSample | bytes32 | The active sample |
| activeSize | uint16 | The active size of the oracle |

### getSampleAt

```solidity
function getSampleAt(Oracle storage oracle, uint16 oracleId, uint40 lookUpTimestamp) internal view returns (uint40 lastUpdate, uint64 cumulativeId, uint64 cumulativeVolatility, uint64 cumulativeBinCrossed)
```

Returns the sample at the given timestamp. If the timestamp is not in the oracle, it returns the closest sample

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| oracle | Oracle storage | The oracle |
| oracleId | uint16 | The oracle id |
| lookUpTimestamp | uint40 | The timestamp to look up |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| lastUpdate | uint40 | The last update timestamp |
| cumulativeId | uint64 | The cumulative id |
| cumulativeVolatility | uint64 | The cumulative volatility |
| cumulativeBinCrossed | uint64 | The cumulative bin crossed |

### binarySearch

```solidity
function binarySearch(Oracle storage oracle, uint16 oracleId, uint40 lookUpTimestamp, uint16 length) internal view returns (bytes32, bytes32)
```

Binary search to find the 2 samples surrounding the given timestamp

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| oracle | Oracle storage | The oracle |
| oracleId | uint16 | The oracle id |
| lookUpTimestamp | uint40 | The timestamp to look up |
| length | uint16 | The oracle length |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| prevSample | bytes32 | The previous sample |
| nextSample | bytes32 | The next sample |

### setSample

```solidity
function setSample(Oracle storage oracle, uint16 oracleId, bytes32 sample) internal checkOracleId(oracleId)
```

Sets the sample at the given oracleId

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| oracle | Oracle storage | The oracle |
| oracleId | uint16 | The oracle id |
| sample | bytes32 | The sample |

### update

```solidity
function update(Oracle storage oracle, bytes32 parameters, uint24 activeId) internal returns (bytes32)
```

Updates the oracle

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| oracle | Oracle storage | The oracle |
| parameters | bytes32 | The parameters |
| activeId | uint24 | The active id |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| Updated parameters | bytes32 | The updated parameters |

### `increaseLength`

```solidity
function increaseLength(Oracle storage oracle, uint16 oracleId, uint16 newLength) internal
```

Increases the oracle length.

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| `oracle` | `Oracle storage` | The oracle |
| `oracleId` | `uint16` | The oracle id |
| `newLength` | `uint16` | The new length |

#### Exceptions

| Name | Description |
| ---- | ----------- |
| `OracleHelper__NewLengthTooSmall` | If `newLength` is smaller than the current oracle length |

#### Return Values

None.