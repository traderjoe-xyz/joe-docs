# OracleHelper
[Git Source](https://github.com/traderjoe-xyz/joe-v2/blob/16f011d25e6bf6d0a0c479974345b623d491104f/src/libraries/OracleHelper.sol)

**Author:**
Trader Joe

This library contains functions to manage the oracle
The oracle samples are stored in a single bytes32 array.
Each sample is encoded as follows:
0 - 16: oracle length (16 bits)
16 - 80: cumulative id (64 bits)
80 - 144: cumulative volatility accumulator (64 bits)
144 - 208: cumulative bin crossed (64 bits)
208 - 216: sample lifetime (8 bits)
216 - 256: sample creation timestamp (40 bits)


## State Variables
### _MAX_SAMPLE_LIFETIME

```solidity
uint256 internal constant _MAX_SAMPLE_LIFETIME = 120 seconds;
```


## Functions
### checkOracleId

*Modifier to check that the oracle id is valid*


```solidity
modifier checkOracleId(uint16 oracleId);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`oracleId`|`uint16`|The oracle id|


### getSample

*Returns the sample at the given oracleId*


```solidity
function getSample(Oracle storage oracle, uint16 oracleId)
    internal
    view
    checkOracleId(oracleId)
    returns (bytes32 sample);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`oracle`|`Oracle`|The oracle|
|`oracleId`|`uint16`|The oracle id|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`sample`|`bytes32`|The sample|


### getActiveSampleAndSize

*Returns the active sample and the active size of the oracle*


```solidity
function getActiveSampleAndSize(Oracle storage oracle, uint16 oracleId)
    internal
    view
    returns (bytes32 activeSample, uint16 activeSize);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`oracle`|`Oracle`|The oracle|
|`oracleId`|`uint16`|The oracle id|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`activeSample`|`bytes32`|The active sample|
|`activeSize`|`uint16`|The active size of the oracle|


### getSampleAt

*Returns the sample at the given timestamp. If the timestamp is not in the oracle, it returns the closest sample*


```solidity
function getSampleAt(Oracle storage oracle, uint16 oracleId, uint40 lookUpTimestamp)
    internal
    view
    returns (uint40 lastUpdate, uint64 cumulativeId, uint64 cumulativeVolatility, uint64 cumulativeBinCrossed);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`oracle`|`Oracle`|The oracle|
|`oracleId`|`uint16`|The oracle id|
|`lookUpTimestamp`|`uint40`|The timestamp to look up|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`lastUpdate`|`uint40`|The last update timestamp|
|`cumulativeId`|`uint64`|The cumulative id|
|`cumulativeVolatility`|`uint64`|The cumulative volatility|
|`cumulativeBinCrossed`|`uint64`|The cumulative bin crossed|


### binarySearch

*Binary search to find the 2 samples surrounding the given timestamp*


```solidity
function binarySearch(Oracle storage oracle, uint16 oracleId, uint40 lookUpTimestamp, uint16 length)
    internal
    view
    returns (bytes32, bytes32);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`oracle`|`Oracle`|The oracle|
|`oracleId`|`uint16`|The oracle id|
|`lookUpTimestamp`|`uint40`|The timestamp to look up|
|`length`|`uint16`|The oracle length|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bytes32`|prevSample The previous sample|
|`<none>`|`bytes32`|nextSample The next sample|


### setSample

*Sets the sample at the given oracleId*


```solidity
function setSample(Oracle storage oracle, uint16 oracleId, bytes32 sample) internal checkOracleId(oracleId);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`oracle`|`Oracle`|The oracle|
|`oracleId`|`uint16`|The oracle id|
|`sample`|`bytes32`|The sample|


### update

*Updates the oracle*


```solidity
function update(Oracle storage oracle, bytes32 parameters, uint24 activeId) internal returns (bytes32);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`oracle`|`Oracle`|The oracle|
|`parameters`|`bytes32`|The parameters|
|`activeId`|`uint24`|The active id|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bytes32`|The updated parameters|


### increaseLength

*Increases the oracle length*


```solidity
function increaseLength(Oracle storage oracle, uint16 oracleId, uint16 newLength) internal;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`oracle`|`Oracle`|The oracle|
|`oracleId`|`uint16`|The oracle id|
|`newLength`|`uint16`|The new length|


### _checkOracleId

*Checks that the oracle id is valid*


```solidity
function _checkOracleId(uint16 oracleId) private pure;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`oracleId`|`uint16`|The oracle id|


## Errors
### OracleHelper__InvalidOracleId

```solidity
error OracleHelper__InvalidOracleId();
```

### OracleHelper__NewLengthTooSmall

```solidity
error OracleHelper__NewLengthTooSmall();
```

### OracleHelper__LookUpTimestampTooOld

```solidity
error OracleHelper__LookUpTimestampTooOld();
```

## Structs
### Oracle

```solidity
struct Oracle {
    bytes32[65535] samples;
}
```

