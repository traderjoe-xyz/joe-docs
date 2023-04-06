## Sample Math

Liquidity Book Sample Math Library

This library contains functions to encode and decode a sample into a single bytes32 and interact with the encoded bytes32
The sample is encoded as follows: <br/>
0 - 16: oracle length (16 bits) <br/>
16 - 80: cumulative id (64 bits)<br/>
80 - 144: cumulative volatility accumulator (64 bits)<br/>
144 - 208: cumulative bin crossed (64 bits)<br/>
208 - 216: sample lifetime (8 bits)<br/>
216 - 256: sample creation timestamp (40 bits)<br/>

### encode

```solidity
function encode(
    uint16 oracleLength,
    uint64 cumulativeId,
    uint64 cumulativeVolatility,
    uint64 cumulativeBinCrossed,
    uint8 sampleLifetime,
    uint40 createdAt
) internal pure returns (bytes32 sample)
```

Encodes a sample

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| oracleLength | uint16 | The oracle length |
| cumulativeId | uint64 | The cumulative id |
| cumulativeVolatility | uint64 | The cumulative volatility |
| cumulativeBinCrossed | uint64 | The cumulative bin crossed |
| sampleLifetime | uint8 | The sample lifetime |
| createdAt | uint40 | The sample creation timestamp |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| sample | bytes32 | The encoded sample |

### getOracleLength

```solidity
function getOracleLength(bytes32 sample) internal pure returns (uint16 length)
```

Gets the oracle length from an encoded sample

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| sample | bytes32 | The encoded sample as follows: <br/>[0 - 16[: oracle length (16 bits) <br/>[16 - 256[: any (240 bits) |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| length | uint16 | The oracle length |

### getCumulativeId

```solidity
function getCumulativeId(bytes32 sample) internal pure returns (uint64 id)
```

Gets the cumulative id from an encoded sample

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| sample | bytes32 | The encoded sample as follows: <br/>[0 - 16[: any (16 bits) <br/>[16 - 80[: cumulative id (64 bits) <br/>[80 - 256[: any (176 bits) |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| id | uint64 | The cumulative id |

### getCumulativeVolatility

```solidity
function getCumulativeVolatility(bytes32 sample) internal pure returns (uint64 volatilityAccumulator)
```

Gets the cumulative volatility accumulator from an encoded sample

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| sample | bytes32 | The encoded sample as follows: <br/>[0 - 80[: any (80 bits) <br/>[80 - 144[: cumulative volatility accumulator (64 bits) <br/>[144 - 256[: any (112 bits) |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| volatilityAccumulator | uint64 | The cumulative volatility |

### getCumulativeBinCrossed

```solidity
function getCumulativeBinCrossed(bytes32 sample) internal pure returns (uint64 binCrossed)
```

Gets the cumulative bin crossed from an encoded sample

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| sample | bytes32 | The encoded sample as follows: <br/>[0 - 144[: any (144 bits) <br/>[144 - 208[: cumulative bin crossed (64 bits) <br/>[208 - 256[: any (48 bits) |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| binCrossed | uint64 | The cumulative bin crossed |

### getSampleLifetime

```solidity
function getSampleLifetime(bytes32 sample) internal pure returns (uint8 lifetime)
```

Gets the sample lifetime from an encoded sample

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| sample | bytes32 | The encoded sample as follows: <br/>[0 - 208[: any (208 bits) <br/>[208 - 216[: sample lifetime (8 bits) <br/>[216 - 256[: any (40 bits) |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| lifetime | uint8 | The sample lifetime |

### getSampleCreation

```solidity
function getSampleCreation(bytes32 sample) internal pure returns (uint40 creation)
```

Gets the sample creation timestamp from an encoded sample

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| sample | bytes32 | The encoded sample as follows: <br/>[0 - 216[: any (216 bits) <br/>[216 - 256[: sample creation timestamp (40 bits) |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| creation | uint40 | The sample creation timestamp |

### getSampleLastUpdate

```solidity
function getSampleLastUpdate(bytes32 sample) internal pure returns (uint40 lastUpdate)
```

Gets the sample last update timestamp from an encoded sample

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| sample | bytes32 | The encoded sample as follows: <br/>[0 - 216[: any (216 bits) <br/>[216 - 256[: sample creation timestamp (40 bits) |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| lastUpdate | uint40 | The sample last update timestamp |

### getWeightedAverage

```solidity
function getWeightedAverage(
    bytes32 sample1,
    bytes32 sample2,
    uint40 weight1,
    uint40 weight2
) internal pure returns (uint64 weightedAverageId, uint64 weightedAverageVolatility, uint64 weightedAverageBinCrossed)
```

Gets the weighted average of two samples and their respective weights

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| sample1 | bytes32 | The first encoded sample |
| sample2 | bytes32 | The second encoded sample |
| weight1 | uint40 | The weight of the first sample |
| weight2 | uint40 | The weight of the second sample |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| weightedAverageId | uint64 | The weighted average id |
| weightedAverageVolatility | uint64 | The weighted average volatility |
| weightedAverageBinCrossed | uint64 | The weighted average bin crossed |

### update

```solidity
function update(bytes32 sample, uint40 deltaTime, uint24 activeId, uint24 volatilityAccumulator, uint24 binCrossed) internal pure returns (uint64 cumulativeId, uint64 cumulativeVolatility, uint64 cumulativeBinCrossed)
```

Updates a sample with the given values

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| sample | bytes32 | The encoded sample |
| deltaTime | uint40 | The time elapsed since the last update |
| activeId | uint24 | The active id |
| volatilityAccumulator | uint24 | The volatility accumulator |
| binCrossed | uint24 | The bin crossed |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| cumulativeId | uint64 | The cumulative id |
| cumulativeVolatility | uint64 | The cumulative volatility |
| cumulativeBinCrossed | uint64 | The cumulative bin crossed |