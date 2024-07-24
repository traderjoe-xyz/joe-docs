## Fee Helper

This library contains functions to calculate fees

### getFeeAmountFrom

```solidity
function getFeeAmountFrom(uint128 amountWithFees, uint128 totalFee) internal pure checkFeeOverflow(totalFee) returns (uint128)
```

Calculates the fee amount from the amount with fees, rounding up

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| amountWithFees | uint128 | The amount with fees |
| totalFee | uint128 | The total fee |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| [0] | uint128 | The fee amount |

### getFeeAmount

```solidity
function getFeeAmount(uint128 amount, uint128 totalFee) internal pure checkFeeOverflow(totalFee) returns (uint128)
```

Calculates the fee amount that will be charged, rounding up

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| amount | uint128 | The amount |
| totalFee | uint128 | The total fee |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| [0] | uint128 | The fee amount |

### getCompositionFee

```solidity
function getCompositionFee(uint128 amountWithFees, uint128 totalFee) internal pure checkFeeOverflow(totalFee) returns (uint128)
```

Calculates the composition fee amount from the amount with fees, rounding down

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| amountWithFees | uint128 | The amount with fees |
| totalFee | uint128 | The total fee |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| [0] | uint128 | The amount with fees |

### getProtocolFeeAmount

```solidity
function getProtocolFeeAmount(uint128 feeAmount, uint128 protocolShare) internal pure checkProtocolShareOverflow(protocolShare) returns (uint128)
```

Calculates the protocol fee amount from the fee amount and the protocol share, rounding down

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| feeAmount | uint128 | The fee amount |
| protocolShare | uint128 | The protocol share |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| [0] | uint128 | The protocol fee amount |
​