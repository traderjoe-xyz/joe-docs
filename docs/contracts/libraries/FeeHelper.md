---
sidebar_position: 0
sidebar_label: 
---

## FeeHelper

Helper contract used for fees calculation

### FeeParameters

```solidity
struct FeeParameters {
  uint16 binStep;
  uint16 baseFactor;
  uint16 filterPeriod;
  uint16 decayPeriod;
  uint16 reductionFactor;
  uint24 variableFeeControl;
  uint16 protocolShare;
  uint24 maxVolatilityAccumulated;
  uint24 volatilityAccumulated;
  uint24 volatilityReference;
  uint24 indexRef;
  uint40 time;
}
```

### FeesDistribution

```solidity
struct FeesDistribution {
  uint128 total;
  uint128 protocol;
}
```

### updateVariableFeeParameters

```solidity
function updateVariableFeeParameters(struct FeeHelper.FeeParameters _fp, uint256 _activeId) internal view
```

Update the value of the volatility accumulated

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _fp | struct FeeHelper.FeeParameters | The current fee parameters |
| _activeId | uint256 | The current active id |

### updateVolatilityAccumulated

```solidity
function updateVolatilityAccumulated(struct FeeHelper.FeeParameters _fp, uint256 _activeId) internal pure
```

Update the volatility accumulated

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _fp | struct FeeHelper.FeeParameters | The fee parameter |
| _activeId | uint256 | The current active id |

### getBaseFee

```solidity
function getBaseFee(struct FeeHelper.FeeParameters _fp) internal pure returns (uint256)
```

Returns the base fee added to a swap, with 18 decimals

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _fp | struct FeeHelper.FeeParameters | The current fee parameters |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| [0] | uint256 | The fee with 18 decimals precision |

### getVariableFee

```solidity
function getVariableFee(struct FeeHelper.FeeParameters _fp) internal pure returns (uint256 variableFee)
```

Returns the variable fee added to a swap, with 18 decimals

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _fp | struct FeeHelper.FeeParameters | The current fee parameters |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| variableFee | uint256 | The variable fee with 18 decimals precision |

### getFeeAmount

```solidity
function getFeeAmount(struct FeeHelper.FeeParameters _fp, uint256 _amount) internal pure returns (uint256)
```

Return the amount of fees added to an amount

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _fp | struct FeeHelper.FeeParameters | The current fee parameter |
| _amount | uint256 | The amount of token sent |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| [0] | uint256 | The fee amount |

### getFeeAmountFrom

```solidity
function getFeeAmountFrom(struct FeeHelper.FeeParameters _fp, uint256 _amountPlusFee) internal pure returns (uint256)
```

Return the fees from an amount

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _fp | struct FeeHelper.FeeParameters | The current fee parameter |
| _amountPlusFee | uint256 | The amount of token sent |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| [0] | uint256 | The fee amount |

### getFeeAmountForC

```solidity
function getFeeAmountForC(struct FeeHelper.FeeParameters _fp, uint256 _amountPlusFee) internal pure returns (uint256)
```

Return the fees added when an user adds liquidity and change the ratio in the active bin

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _fp | struct FeeHelper.FeeParameters | The current fee parameter |
| _amountPlusFee | uint256 | The amount of token sent |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| [0] | uint256 | The fee amount |

### getFeeAmountDistribution

```solidity
function getFeeAmountDistribution(struct FeeHelper.FeeParameters _fp, uint256 _fees) internal pure returns (struct FeeHelper.FeesDistribution fees)
```

Return the fees distribution added to an amount

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _fp | struct FeeHelper.FeeParameters | The current fee parameter |
| _fees | uint256 | The fee amount |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| fees | struct FeeHelper.FeesDistribution | The fee distribution |

### getTotalFee

```solidity
function getTotalFee(struct FeeHelper.FeeParameters _fp) private pure returns (uint256)
```

Return the total fee, i.e. baseFee + variableFee

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _fp | struct FeeHelper.FeeParameters | The current fee parameter |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| [0] | uint256 | The total fee, with 18 decimals |

