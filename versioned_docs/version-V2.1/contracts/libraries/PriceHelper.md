## PriceHelper

This library contains functions to calculate prices

### getPriceFromId

```solidity
function getPriceFromId(uint24 id, uint16 binStep) internal pure returns (uint256)
```

Calculates the price from the id and the bin step

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| id | uint24 | The id |
| binStep | uint16 | The bin step |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| price | uint256 | The price as a 128.128-binary fixed-point number |

### getIdFromPrice

```solidity
function getIdFromPrice(uint256 price, uint16 binStep) internal pure returns (uint24)
```

Calculates the id from the price and the bin step

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| price | uint256 | The price as a 128.128-binary fixed-point number |
| binStep | uint16 | The bin step |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| id | uint24 | The id |

### getBase

```solidity
function getBase(uint16 binStep) internal pure returns (uint256)
```

Calculates the base from the bin step, which is `1 + binStep / BASIS_POINT_MAX`.

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| binStep | uint16 | The bin step |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| base | uint256 | The base |

### getExponent

```solidity
function getExponent(uint24 id) internal pure returns (int256)
```

Calculates the exponent from the id, which is `id - REAL_ID_SHIFT`.

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| id | uint24 | The id |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| exponent | int256 | The exponent |

### convertDecimalPriceTo128x128

```solidity
function convertDecimalPriceTo128x128(uint256 price) internal pure returns (uint256)
```

Converts a price with 18 decimals to a 128.128-binary fixed-point number

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| price | uint256 | The price with 18 decimals |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| price128x128 | uint256 | The 128.128-binary fixed-point number |

### convert128x128PriceToDecimal

```solidity
function convert128x128PriceToDecimal(uint256 price128x128) internal pure returns (uint256)
```

Converts a 128.128-binary fixed-point number to a price with 18 decimals

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| price128x128 | uint256 | The 128.128-binary fixed-point number |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| price | uint256 | The price with 18 decimals |