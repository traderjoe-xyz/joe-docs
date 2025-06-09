# SampleMath
[Git Source](https://github.com/lfj-gg/joe-v2/blob/16f011d25e6bf6d0a0c479974345b623d491104f/src/libraries/math/SampleMath.sol)

**Author:**
Trader Joe

This library contains functions to encode and decode a sample into a single bytes32
and interact with the encoded bytes32
The sample is encoded as follows:
0 - 16: oracle length (16 bits)
16 - 80: cumulative id (64 bits)
80 - 144: cumulative volatility accumulator (64 bits)
144 - 208: cumulative bin crossed (64 bits)
208 - 216: sample lifetime (8 bits)
216 - 256: sample creation timestamp (40 bits)


## State Variables
### OFFSET_ORACLE_LENGTH

```solidity
uint256 internal constant OFFSET_ORACLE_LENGTH = 0;
```


### OFFSET_CUMULATIVE_ID

```solidity
uint256 internal constant OFFSET_CUMULATIVE_ID = 16;
```


### OFFSET_CUMULATIVE_VOLATILITY

```solidity
uint256 internal constant OFFSET_CUMULATIVE_VOLATILITY = 80;
```


### OFFSET_CUMULATIVE_BIN_CROSSED

```solidity
uint256 internal constant OFFSET_CUMULATIVE_BIN_CROSSED = 144;
```


### OFFSET_SAMPLE_LIFETIME

```solidity
uint256 internal constant OFFSET_SAMPLE_LIFETIME = 208;
```


### OFFSET_SAMPLE_CREATION

```solidity
uint256 internal constant OFFSET_SAMPLE_CREATION = 216;
```


## Functions
### encode

*Encodes a sample*


```solidity
function encode(
    uint16 oracleLength,
    uint64 cumulativeId,
    uint64 cumulativeVolatility,
    uint64 cumulativeBinCrossed,
    uint8 sampleLifetime,
    uint40 createdAt
) internal pure returns (bytes32 sample);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`oracleLength`|`uint16`|The oracle length|
|`cumulativeId`|`uint64`|The cumulative id|
|`cumulativeVolatility`|`uint64`|The cumulative volatility|
|`cumulativeBinCrossed`|`uint64`|The cumulative bin crossed|
|`sampleLifetime`|`uint8`|The sample lifetime|
|`createdAt`|`uint40`|The sample creation timestamp|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`sample`|`bytes32`|The encoded sample|


### getOracleLength

*Gets the oracle length from an encoded sample*


```solidity
function getOracleLength(bytes32 sample) internal pure returns (uint16 length);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`sample`|`bytes32`|The encoded sample as follows: [0 - 16[: oracle length (16 bits) [16 - 256[: any (240 bits)|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`length`|`uint16`|The oracle length|


### getCumulativeId

*Gets the cumulative id from an encoded sample*


```solidity
function getCumulativeId(bytes32 sample) internal pure returns (uint64 id);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`sample`|`bytes32`|The encoded sample as follows: [0 - 16[: any (16 bits) [16 - 80[: cumulative id (64 bits) [80 - 256[: any (176 bits)|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`id`|`uint64`|The cumulative id|


### getCumulativeVolatility

*Gets the cumulative volatility accumulator from an encoded sample*


```solidity
function getCumulativeVolatility(bytes32 sample) internal pure returns (uint64 volatilityAccumulator);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`sample`|`bytes32`|The encoded sample as follows: [0 - 80[: any (80 bits) [80 - 144[: cumulative volatility accumulator (64 bits) [144 - 256[: any (112 bits)|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`volatilityAccumulator`|`uint64`|The cumulative volatility|


### getCumulativeBinCrossed

*Gets the cumulative bin crossed from an encoded sample*


```solidity
function getCumulativeBinCrossed(bytes32 sample) internal pure returns (uint64 binCrossed);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`sample`|`bytes32`|The encoded sample as follows: [0 - 144[: any (144 bits) [144 - 208[: cumulative bin crossed (64 bits) [208 - 256[: any (48 bits)|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`binCrossed`|`uint64`|The cumulative bin crossed|


### getSampleLifetime

*Gets the sample lifetime from an encoded sample*


```solidity
function getSampleLifetime(bytes32 sample) internal pure returns (uint8 lifetime);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`sample`|`bytes32`|The encoded sample as follows: [0 - 208[: any (208 bits) [208 - 216[: sample lifetime (8 bits) [216 - 256[: any (40 bits)|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`lifetime`|`uint8`|The sample lifetime|


### getSampleCreation

*Gets the sample creation timestamp from an encoded sample*


```solidity
function getSampleCreation(bytes32 sample) internal pure returns (uint40 creation);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`sample`|`bytes32`|The encoded sample as follows: [0 - 216[: any (216 bits) [216 - 256[: sample creation timestamp (40 bits)|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`creation`|`uint40`|The sample creation timestamp|


### getSampleLastUpdate

*Gets the sample last update timestamp from an encoded sample*


```solidity
function getSampleLastUpdate(bytes32 sample) internal pure returns (uint40 lastUpdate);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`sample`|`bytes32`|The encoded sample as follows: [0 - 216[: any (216 bits) [216 - 256[: sample creation timestamp (40 bits)|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`lastUpdate`|`uint40`|The sample last update timestamp|


### getWeightedAverage

*Gets the weighted average of two samples and their respective weights*


```solidity
function getWeightedAverage(bytes32 sample1, bytes32 sample2, uint40 weight1, uint40 weight2)
    internal
    pure
    returns (uint64 weightedAverageId, uint64 weightedAverageVolatility, uint64 weightedAverageBinCrossed);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`sample1`|`bytes32`|The first encoded sample|
|`sample2`|`bytes32`|The second encoded sample|
|`weight1`|`uint40`|The weight of the first sample|
|`weight2`|`uint40`|The weight of the second sample|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`weightedAverageId`|`uint64`|The weighted average id|
|`weightedAverageVolatility`|`uint64`|The weighted average volatility|
|`weightedAverageBinCrossed`|`uint64`|The weighted average bin crossed|


### update

*Updates a sample with the given values*


```solidity
function update(bytes32 sample, uint40 deltaTime, uint24 activeId, uint24 volatilityAccumulator, uint24 binCrossed)
    internal
    pure
    returns (uint64 cumulativeId, uint64 cumulativeVolatility, uint64 cumulativeBinCrossed);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`sample`|`bytes32`|The encoded sample|
|`deltaTime`|`uint40`|The time elapsed since the last update|
|`activeId`|`uint24`|The active id|
|`volatilityAccumulator`|`uint24`|The volatility accumulator|
|`binCrossed`|`uint24`|The bin crossed|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`cumulativeId`|`uint64`|The cumulative id|
|`cumulativeVolatility`|`uint64`|The cumulative volatility|
|`cumulativeBinCrossed`|`uint64`|The cumulative bin crossed|


