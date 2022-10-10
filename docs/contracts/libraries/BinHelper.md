---
sidebar_position: 0
sidebar_label: 
---

## BinHelper

Contract used to convert bin ID to price and back

### getIdFromPrice

```solidity
function getIdFromPrice(uint256 _price, uint256 _binStep) internal pure returns (uint24)
```

Returns the id corresponding to the given price

_The id may be inaccurate due to rounding issues, always trust getPriceFromId rather than
getIdFromPrice_

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _price | uint256 | The price of y per x as a 128.128-binary fixed-point number |
| _binStep | uint256 | The bin step |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| [0] | uint24 | The id corresponding to this price |

### getPriceFromId

```solidity
function getPriceFromId(uint256 _id, uint256 _binStep) internal pure returns (uint256)
```

Returns the price corresponding to the given ID, as a 128.128-binary fixed-point number

_This is the trusted function to link id to price, the other way may be inaccurate_

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _id | uint256 | The id |
| _binStep | uint256 | The bin step |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| [0] | uint256 | The price corresponding to this id, as a 128.128-binary fixed-point number |

### _getBPValue

```solidity
function _getBPValue(uint256 _binStep) internal pure returns (uint256)
```

Returns the (1 + bp) value as a 128.128-decimal fixed-point number

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _binStep | uint256 | The bp value in [1; 100] (referring to 0.01% to 1%) |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| [0] | uint256 | The (1+bp) value as a 128.128-decimal fixed-point number |

