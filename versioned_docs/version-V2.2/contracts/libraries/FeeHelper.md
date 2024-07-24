# FeeHelper
[Git Source](https://github.com/traderjoe-xyz/joe-v2/blob/16f011d25e6bf6d0a0c479974345b623d491104f/src/libraries/FeeHelper.sol)

**Author:**
Trader Joe

This library contains functions to calculate fees


## Functions
### verifyFee

*Modifier to check that the fee is not too large*


```solidity
modifier verifyFee(uint128 fee);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`fee`|`uint128`|The fee|


### verifyProtocolShare

*Modifier to check that the protocol share is not too large*


```solidity
modifier verifyProtocolShare(uint128 protocolShare);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`protocolShare`|`uint128`|The protocol share|


### getFeeAmountFrom

*Calculates the fee amount from the amount with fees, rounding up*


```solidity
function getFeeAmountFrom(uint128 amountWithFees, uint128 totalFee)
    internal
    pure
    verifyFee(totalFee)
    returns (uint128);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`amountWithFees`|`uint128`|The amount with fees|
|`totalFee`|`uint128`|The total fee|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint128`|feeAmount The fee amount|


### getFeeAmount

*Calculates the fee amount that will be charged, rounding up*


```solidity
function getFeeAmount(uint128 amount, uint128 totalFee) internal pure verifyFee(totalFee) returns (uint128);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`amount`|`uint128`|The amount|
|`totalFee`|`uint128`|The total fee|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint128`|feeAmount The fee amount|


### getCompositionFee

*Calculates the composition fee amount from the amount with fees, rounding down*


```solidity
function getCompositionFee(uint128 amountWithFees, uint128 totalFee)
    internal
    pure
    verifyFee(totalFee)
    returns (uint128);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`amountWithFees`|`uint128`|The amount with fees|
|`totalFee`|`uint128`|The total fee|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint128`|The amount with fees|


### getProtocolFeeAmount

*Calculates the protocol fee amount from the fee amount and the protocol share, rounding down*


```solidity
function getProtocolFeeAmount(uint128 feeAmount, uint128 protocolShare)
    internal
    pure
    verifyProtocolShare(protocolShare)
    returns (uint128);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`feeAmount`|`uint128`|The fee amount|
|`protocolShare`|`uint128`|The protocol share|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint128`|protocolFeeAmount The protocol fee amount|


### _verifyFee

*Internal function to check that the fee is not too large*


```solidity
function _verifyFee(uint128 fee) private pure;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`fee`|`uint128`|The fee|


## Errors
### FeeHelper__FeeTooLarge

```solidity
error FeeHelper__FeeTooLarge();
```

### FeeHelper__ProtocolShareTooLarge

```solidity
error FeeHelper__ProtocolShareTooLarge();
```

