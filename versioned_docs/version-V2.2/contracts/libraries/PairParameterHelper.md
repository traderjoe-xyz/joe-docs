# PairParameterHelper
[Git Source](https://github.com/traderjoe-xyz/joe-v2/blob/16f011d25e6bf6d0a0c479974345b623d491104f/src/libraries/PairParameterHelper.sol)

**Author:**
Trader Joe

*This library contains functions to get and set parameters of a pair
The parameters are stored in a single bytes32 variable in the following format:
[0 - 16[: base factor (16 bits)
[16 - 28[: filter period (12 bits)
[28 - 40[: decay period (12 bits)
[40 - 54[: reduction factor (14 bits)
[54 - 78[: variable fee control (24 bits)
[78 - 92[: protocol share (14 bits)
[92 - 112[: max volatility accumulator (20 bits)
[112 - 132[: volatility accumulator (20 bits)
[132 - 152[: volatility reference (20 bits)
[152 - 176[: index reference (24 bits)
[176 - 216[: time of last update (40 bits)
[216 - 232[: oracle index (16 bits)
[232 - 256[: active index (24 bits)*


## State Variables
### OFFSET_BASE_FACTOR

```solidity
uint256 internal constant OFFSET_BASE_FACTOR = 0;
```


### OFFSET_FILTER_PERIOD

```solidity
uint256 internal constant OFFSET_FILTER_PERIOD = 16;
```


### OFFSET_DECAY_PERIOD

```solidity
uint256 internal constant OFFSET_DECAY_PERIOD = 28;
```


### OFFSET_REDUCTION_FACTOR

```solidity
uint256 internal constant OFFSET_REDUCTION_FACTOR = 40;
```


### OFFSET_VAR_FEE_CONTROL

```solidity
uint256 internal constant OFFSET_VAR_FEE_CONTROL = 54;
```


### OFFSET_PROTOCOL_SHARE

```solidity
uint256 internal constant OFFSET_PROTOCOL_SHARE = 78;
```


### OFFSET_MAX_VOL_ACC

```solidity
uint256 internal constant OFFSET_MAX_VOL_ACC = 92;
```


### OFFSET_VOL_ACC

```solidity
uint256 internal constant OFFSET_VOL_ACC = 112;
```


### OFFSET_VOL_REF

```solidity
uint256 internal constant OFFSET_VOL_REF = 132;
```


### OFFSET_ID_REF

```solidity
uint256 internal constant OFFSET_ID_REF = 152;
```


### OFFSET_TIME_LAST_UPDATE

```solidity
uint256 internal constant OFFSET_TIME_LAST_UPDATE = 176;
```


### OFFSET_ORACLE_ID

```solidity
uint256 internal constant OFFSET_ORACLE_ID = 216;
```


### OFFSET_ACTIVE_ID

```solidity
uint256 internal constant OFFSET_ACTIVE_ID = 232;
```


### MASK_STATIC_PARAMETER

```solidity
uint256 internal constant MASK_STATIC_PARAMETER = 0xffffffffffffffffffffffffffff;
```


## Functions
### getBaseFactor

*Get the base factor from the encoded pair parameters*


```solidity
function getBaseFactor(bytes32 params) internal pure returns (uint16 baseFactor);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`params`|`bytes32`|The encoded pair parameters, as follows: [0 - 16[: base factor (16 bits) [16 - 256[: other parameters|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`baseFactor`|`uint16`|The base factor|


### getFilterPeriod

*Get the filter period from the encoded pair parameters*


```solidity
function getFilterPeriod(bytes32 params) internal pure returns (uint16 filterPeriod);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`params`|`bytes32`|The encoded pair parameters, as follows: [0 - 16[: other parameters [16 - 28[: filter period (12 bits) [28 - 256[: other parameters|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`filterPeriod`|`uint16`|The filter period|


### getDecayPeriod

*Get the decay period from the encoded pair parameters*


```solidity
function getDecayPeriod(bytes32 params) internal pure returns (uint16 decayPeriod);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`params`|`bytes32`|The encoded pair parameters, as follows: [0 - 28[: other parameters [28 - 40[: decay period (12 bits) [40 - 256[: other parameters|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`decayPeriod`|`uint16`|The decay period|


### getReductionFactor

*Get the reduction factor from the encoded pair parameters*


```solidity
function getReductionFactor(bytes32 params) internal pure returns (uint16 reductionFactor);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`params`|`bytes32`|The encoded pair parameters, as follows: [0 - 40[: other parameters [40 - 54[: reduction factor (14 bits) [54 - 256[: other parameters|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`reductionFactor`|`uint16`|The reduction factor|


### getVariableFeeControl

*Get the variable fee control from the encoded pair parameters*


```solidity
function getVariableFeeControl(bytes32 params) internal pure returns (uint24 variableFeeControl);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`params`|`bytes32`|The encoded pair parameters, as follows: [0 - 54[: other parameters [54 - 78[: variable fee control (24 bits) [78 - 256[: other parameters|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`variableFeeControl`|`uint24`|The variable fee control|


### getProtocolShare

*Get the protocol share from the encoded pair parameters*


```solidity
function getProtocolShare(bytes32 params) internal pure returns (uint16 protocolShare);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`params`|`bytes32`|The encoded pair parameters, as follows: [0 - 78[: other parameters [78 - 92[: protocol share (14 bits) [92 - 256[: other parameters|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`protocolShare`|`uint16`|The protocol share|


### getMaxVolatilityAccumulator

*Get the max volatility accumulator from the encoded pair parameters*


```solidity
function getMaxVolatilityAccumulator(bytes32 params) internal pure returns (uint24 maxVolatilityAccumulator);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`params`|`bytes32`|The encoded pair parameters, as follows: [0 - 92[: other parameters [92 - 112[: max volatility accumulator (20 bits) [112 - 256[: other parameters|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`maxVolatilityAccumulator`|`uint24`|The max volatility accumulator|


### getVolatilityAccumulator

*Get the volatility accumulator from the encoded pair parameters*


```solidity
function getVolatilityAccumulator(bytes32 params) internal pure returns (uint24 volatilityAccumulator);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`params`|`bytes32`|The encoded pair parameters, as follows: [0 - 112[: other parameters [112 - 132[: volatility accumulator (20 bits) [132 - 256[: other parameters|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`volatilityAccumulator`|`uint24`|The volatility accumulator|


### getVolatilityReference

*Get the volatility reference from the encoded pair parameters*


```solidity
function getVolatilityReference(bytes32 params) internal pure returns (uint24 volatilityReference);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`params`|`bytes32`|The encoded pair parameters, as follows: [0 - 132[: other parameters [132 - 152[: volatility reference (20 bits) [152 - 256[: other parameters|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`volatilityReference`|`uint24`|The volatility reference|


### getIdReference

*Get the index reference from the encoded pair parameters*


```solidity
function getIdReference(bytes32 params) internal pure returns (uint24 idReference);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`params`|`bytes32`|The encoded pair parameters, as follows: [0 - 152[: other parameters [152 - 176[: index reference (24 bits) [176 - 256[: other parameters|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`idReference`|`uint24`|The index reference|


### getTimeOfLastUpdate

*Get the time of last update from the encoded pair parameters*


```solidity
function getTimeOfLastUpdate(bytes32 params) internal pure returns (uint40 timeOflastUpdate);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`params`|`bytes32`|The encoded pair parameters, as follows: [0 - 176[: other parameters [176 - 216[: time of last update (40 bits) [216 - 256[: other parameters|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`timeOflastUpdate`|`uint40`|The time of last update|


### getOracleId

*Get the oracle id from the encoded pair parameters*


```solidity
function getOracleId(bytes32 params) internal pure returns (uint16 oracleId);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`params`|`bytes32`|The encoded pair parameters, as follows: [0 - 216[: other parameters [216 - 232[: oracle id (16 bits) [232 - 256[: other parameters|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`oracleId`|`uint16`|The oracle id|


### getActiveId

*Get the active index from the encoded pair parameters*


```solidity
function getActiveId(bytes32 params) internal pure returns (uint24 activeId);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`params`|`bytes32`|The encoded pair parameters, as follows: [0 - 232[: other parameters [232 - 256[: active index (24 bits)|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`activeId`|`uint24`|The active index|


### getDeltaId

*Get the delta between the current active index and the cached active index*


```solidity
function getDeltaId(bytes32 params, uint24 activeId) internal pure returns (uint24);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`params`|`bytes32`|The encoded pair parameters, as follows: [0 - 232[: other parameters [232 - 256[: active index (24 bits)|
|`activeId`|`uint24`|The current active index|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint24`|The delta|


### getBaseFee

*Calculates the base fee, with 18 decimals*


```solidity
function getBaseFee(bytes32 params, uint16 binStep) internal pure returns (uint256);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`params`|`bytes32`|The encoded pair parameters|
|`binStep`|`uint16`|The bin step (in basis points)|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint256`|baseFee The base fee|


### getVariableFee

*Calculates the variable fee*


```solidity
function getVariableFee(bytes32 params, uint16 binStep) internal pure returns (uint256 variableFee);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`params`|`bytes32`|The encoded pair parameters|
|`binStep`|`uint16`|The bin step (in basis points)|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`variableFee`|`uint256`|The variable fee|


### getTotalFee

*Calculates the total fee, which is the sum of the base fee and the variable fee*


```solidity
function getTotalFee(bytes32 params, uint16 binStep) internal pure returns (uint128);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`params`|`bytes32`|The encoded pair parameters|
|`binStep`|`uint16`|The bin step (in basis points)|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint128`|totalFee The total fee|


### setOracleId

*Set the oracle id in the encoded pair parameters*


```solidity
function setOracleId(bytes32 params, uint16 oracleId) internal pure returns (bytes32);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`params`|`bytes32`|The encoded pair parameters|
|`oracleId`|`uint16`|The oracle id|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bytes32`|The updated encoded pair parameters|


### setVolatilityReference

*Set the volatility reference in the encoded pair parameters*


```solidity
function setVolatilityReference(bytes32 params, uint24 volRef) internal pure returns (bytes32);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`params`|`bytes32`|The encoded pair parameters|
|`volRef`|`uint24`|The volatility reference|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bytes32`|The updated encoded pair parameters|


### setVolatilityAccumulator

*Set the volatility accumulator in the encoded pair parameters*


```solidity
function setVolatilityAccumulator(bytes32 params, uint24 volAcc) internal pure returns (bytes32);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`params`|`bytes32`|The encoded pair parameters|
|`volAcc`|`uint24`|The volatility accumulator|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bytes32`|The updated encoded pair parameters|


### setActiveId

*Set the active id in the encoded pair parameters*


```solidity
function setActiveId(bytes32 params, uint24 activeId) internal pure returns (bytes32 newParams);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`params`|`bytes32`|The encoded pair parameters|
|`activeId`|`uint24`|The active id|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`newParams`|`bytes32`|The updated encoded pair parameters|


### setStaticFeeParameters

*Sets the static fee parameters in the encoded pair parameters*


```solidity
function setStaticFeeParameters(
    bytes32 params,
    uint16 baseFactor,
    uint16 filterPeriod,
    uint16 decayPeriod,
    uint16 reductionFactor,
    uint24 variableFeeControl,
    uint16 protocolShare,
    uint24 maxVolatilityAccumulator
) internal pure returns (bytes32 newParams);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`params`|`bytes32`|The encoded pair parameters|
|`baseFactor`|`uint16`|The base factor|
|`filterPeriod`|`uint16`|The filter period|
|`decayPeriod`|`uint16`|The decay period|
|`reductionFactor`|`uint16`|The reduction factor|
|`variableFeeControl`|`uint24`|The variable fee control|
|`protocolShare`|`uint16`|The protocol share|
|`maxVolatilityAccumulator`|`uint24`|The max volatility accumulator|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`newParams`|`bytes32`|The updated encoded pair parameters|


### updateIdReference

*Updates the index reference in the encoded pair parameters*


```solidity
function updateIdReference(bytes32 params) internal pure returns (bytes32 newParams);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`params`|`bytes32`|The encoded pair parameters|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`newParams`|`bytes32`|The updated encoded pair parameters|


### updateTimeOfLastUpdate

*Updates the time of last update in the encoded pair parameters*


```solidity
function updateTimeOfLastUpdate(bytes32 params, uint256 timestamp) internal pure returns (bytes32 newParams);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`params`|`bytes32`|The encoded pair parameters|
|`timestamp`|`uint256`|The timestamp|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`newParams`|`bytes32`|The updated encoded pair parameters|


### updateVolatilityReference

*Updates the volatility reference in the encoded pair parameters*


```solidity
function updateVolatilityReference(bytes32 params) internal pure returns (bytes32);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`params`|`bytes32`|The encoded pair parameters|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bytes32`|The updated encoded pair parameters|


### updateVolatilityAccumulator

*Updates the volatility accumulator in the encoded pair parameters*


```solidity
function updateVolatilityAccumulator(bytes32 params, uint24 activeId) internal pure returns (bytes32);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`params`|`bytes32`|The encoded pair parameters|
|`activeId`|`uint24`|The active id|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bytes32`|The updated encoded pair parameters|


### updateReferences

*Updates the volatility reference and the volatility accumulator in the encoded pair parameters*


```solidity
function updateReferences(bytes32 params, uint256 timestamp) internal pure returns (bytes32);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`params`|`bytes32`|The encoded pair parameters|
|`timestamp`|`uint256`|The timestamp|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bytes32`|The updated encoded pair parameters|


### updateVolatilityParameters

*Updates the volatility reference and the volatility accumulator in the encoded pair parameters*


```solidity
function updateVolatilityParameters(bytes32 params, uint24 activeId, uint256 timestamp)
    internal
    pure
    returns (bytes32);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`params`|`bytes32`|The encoded pair parameters|
|`activeId`|`uint24`|The active id|
|`timestamp`|`uint256`|The timestamp|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bytes32`|The updated encoded pair parameters|


## Errors
### PairParametersHelper__InvalidParameter

```solidity
error PairParametersHelper__InvalidParameter();
```

