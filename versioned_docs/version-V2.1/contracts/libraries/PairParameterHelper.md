## Pair Parameter Helper

Liquidity Book Pair Parameter Helper Library - This library contains functions to get and set parameters of a pair

The parameters are stored in a single bytes32 variable. 

```solidity
library PairParameterHelper {
```

### getBaseFactor

```solidity
function getBaseFactor(bytes32 params) internal pure returns (uint16 baseFactor)
```

Get the base factor from the encoded pair parameters

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| params | bytes32 | The encoded pair parameters |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| baseFactor | uint16 | The base factor |

### getFilterPeriod

```solidity
function getFilterPeriod(bytes32 params) internal pure returns (uint16 filterPeriod)
```

Get the filter period from the encoded pair parameters

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| params | bytes32 | The encoded pair parameters |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| filterPeriod | uint16 | The filter period |

### getDecayPeriod

```solidity
function getDecayPeriod(bytes32 params) internal pure returns (uint16 decayPeriod)
```

Get the decay period from the encoded pair parameters

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| params | bytes32 | The encoded pair parameters |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| decayPeriod | uint16 | The decay period |

### getReductionFactor

```solidity
function getReductionFactor(bytes32 params) internal pure returns (uint16 reductionFactor)
```

Get the reduction factor from the encoded pair parameters

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| params | bytes32 | The encoded pair parameters |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| reductionFactor | uint16 | The reduction factor |

### getVariableFeeControl

```solidity
function getVariableFeeControl(bytes32 params) internal pure returns (uint24 variableFeeControl)
```

Get the variable fee control from the encoded pair parameters

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| params | bytes32 | The encoded pair parameters |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| variableFeeControl | uint24 | The variable fee control |

### getProtocolShare

```solidity
function getProtocolShare(bytes32 params) internal pure returns (uint16 protocolShare)
```

Get the protocol share from the encoded pair parameters

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| params | bytes32 | The encoded pair parameters |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| protocolShare | uint16 | The protocol share |

### getMaxVolatilityAccumulator

```solidity
function getMaxVolatilityAccumulator(bytes32 params) internal pure returns (uint24 maxVolatilityAccumulator)
```

Get the max volatility accumulator from the encoded pair parameters

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| params | bytes32 | The encoded pair parameters |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| maxVolatilityAccumulator | uint24 | The max volatility accumulator |

### getVolatilityAccumulator

```solidity
function getVolatilityAccumulator(bytes32 params) internal pure returns (uint24 volatilityAccumulator)
```

Get the volatility accumulator from the encoded pair parameters

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| params | bytes32 | The encoded pair parameters |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| volatilityAccumulator | uint24 | The volatility accumulator |

### getVolatilityReference

```solidity
function getVolatilityReference(bytes32 params) internal pure returns (uint24 volatilityReference)
```

Get the volatility reference from the encoded pair parameters

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| params | bytes32 | The encoded pair parameters |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| volatilityReference | uint24 | The volatility reference |

### getIdReference

```solidity
function getIdReference(bytes32 params) internal pure returns (uint24 idReference)
```

Get the index reference from the encoded pair parameters

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| params | bytes32 | The encoded pair parameters |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| idReference | uint24 | The index reference |

### getTimeOfLastUpdate

```solidity
function getTimeOfLastUpdate(bytes32 params) internal pure returns (uint40 timeOflastUpdate)
```

Get the time of last update from the encoded pair parameters

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| params | bytes32 | The encoded pair parameters |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| timeOflastUpdate | uint40 | The time of last update |

### getOracleId

```solidity
function getOracleId(bytes32 params) internal pure returns (uint16 oracleId)
```

Get the oracle id from the encoded pair parameters

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| params | bytes32 | The encoded pair parameters |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| oracleId | uint16 | The oracle id |

### getActiveId

```solidity
function getActiveId(bytes32 params) internal pure returns (uint24 activeId)
```

Get the active index from the encoded pair parameters.

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| params | bytes32 | The encoded pair parameters |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| activeId | uint24 | The active index |

### getDeltaId

```solidity
function getDeltaId(bytes32 params, uint24 activeId) internal pure returns (uint24)
```

Get the delta between the active index and the reference index.

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| params | bytes32 | The encoded pair parameters |
| activeId | uint24 | The active index |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
|  |  | The delta |

### getBaseFee

```solidity
function getBaseFee(bytes32 params, uint16 binStep) internal pure returns (uint256)
```

Calculates the base fee, with 18 decimals.

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| params | bytes32 | The encoded pair parameters |
| binStep | uint16 | The bin step (in basis points) |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
|  |  | The base fee |

### getVariableFee

```solidity
function getVariableFee(bytes32 params, uint16 binStep) internal pure returns (uint256 variableFee)
```

Calculates the variable fee.

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| params | bytes32 | The encoded pair parameters |
| binStep | uint16 | The bin step (in basis points) |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| variableFee | uint256 | The variable fee |

### getTotalFee

```solidity
function getTotalFee(bytes32 params, uint16 binStep) internal pure returns (uint128)
```

Calculates the total fee, which is the sum of the base fee and the variable fee.

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| params | bytes32 | The encoded pair parameters |
| binStep | uint16 | The bin step (in basis points) |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
|  |  | The total fee |

### setOracleId

```solidity
function setOracleId(bytes32 params, uint16 oracleId) internal pure returns (bytes32)
```

Set the oracle id in the encoded pair parameters.

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| params | bytes32 | The encoded pair parameters |
| oracleId | uint16 | The oracle id |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
|  | bytes32 | The updated encoded pair parameters |

### setVolatilityReference

```solidity
function setVolatilityReference(bytes32 params, uint24 volRef) internal pure returns (bytes32)
```

Set the volatility reference in the encoded pair parameters.

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| params | bytes32 | The encoded pair parameters |
| volRef | uint24 | The volatility reference |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
|  | bytes32 | The updated encoded pair parameters |

### setVolatilityAccumulator

```solidity
function setVolatilityAccumulator(bytes32 params, uint24 volAcc) internal pure returns (bytes32)
```

Set the volatility accumulator in the encoded pair parameters.

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| params | bytes32 | The encoded pair parameters |
| volAcc | uint24 | The volatility accumulator |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
|  | bytes32 | The updated encoded pair parameters |

### setActiveId

```solidity
function setActiveId(bytes32 params, uint24 activeId) internal pure returns (bytes32 newParams)
```

Set the active id in the encoded pair parameters.

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| params | bytes32 | The encoded pair parameters |
| activeId | uint24 | The active id |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| newParams | bytes32 | The updated encoded pair parameters |

### setStaticFeeParameters

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
) internal pure returns (bytes32 newParams)
```

Sets the static fee parameters in the encoded pair parameters.

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| params | bytes32 | The encoded pair parameters |
| baseFactor | uint16 | The base factor |
| filterPeriod | uint16 | The filter period |
| decayPeriod | uint16 | The decay period |
| reductionFactor | uint16 | The reduction factor |
| variableFeeControl | uint24 | The variable fee control |
| protocolShare | uint16 | The protocol share |
| maxVolatilityAccumulator | uint24 | The max volatility accumulator |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| newParams | bytes32 | The updated encoded pair parameters |

### updateIdReference

```solidity
function updateIdReference(bytes32 params) internal pure returns (bytes32 newParams)
```

Updates the index reference in the encoded pair parameters.

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| params | bytes32 | The encoded pair parameters |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| newParams | bytes32 | The updated encoded pair parameters |

### updateTimeOfLastUpdate

```solidity
function updateTimeOfLastUpdate(bytes32 params) internal view returns (bytes32 newParams)
```

Updates the time of last update in the encoded pair parameters.

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| params | bytes32 | The encoded pair parameters |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| newParams | bytes32 | The updated encoded pair parameters |

### updateVolatilityReference

```solidity
function updateVolatilityReference(bytes32 params) internal pure returns (bytes32)
```

Updates the volatility reference in the encoded pair parameters.

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| params | bytes32 | The encoded pair parameters |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| | bytes32 | The updated encoded pair parameters |

### updateVolatilityAccumulator

```solidity
function updateVolatilityAccumulator(bytes32 params, uint24 activeId) internal pure returns (bytes32)
```

Updates the volatility accumulator in the encoded pair parameters.

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| params | bytes32 | The encoded pair parameters |
| activeId | uint24 | The active id |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| | bytes32 | The updated encoded pair parameters |

### updateReferences

```solidity
function updateReferences(bytes32 params) internal view returns (bytes32)
```

Updates the volatility reference and the volatility accumulator in the encoded pair parameters.

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| params | bytes32 | The encoded pair parameters |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| | bytes32 | The updated encoded pair parameters |

### updateVolatilityParameters

```solidity
function updateVolatilityParameters(bytes32 params, uint24 activeId) internal view returns (bytes32)
```

Updates the volatility reference and the volatility accumulator in the encoded pair parameters.

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| params | bytes32 | The encoded pair parameters |
| activeId | uint24 | The active id |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| | bytes32 | The updated encoded pair parameters |