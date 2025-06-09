# Uint256x256Math
[Git Source](https://github.com/lfj-gg/joe-v2/blob/16f011d25e6bf6d0a0c479974345b623d491104f/src/libraries/math/Uint256x256Math.sol)

**Author:**
Trader Joe

Helper contract used for full precision calculations


## Functions
### mulDivRoundDown

Calculates floor(x*y/denominator) with full precision
The result will be rounded down

*Credit to Remco Bloemen under MIT license https://xn--2-umb.com/21/muldiv
Requirements:
- The denominator cannot be zero
- The result must fit within uint256
Caveats:
- This function does not work with fixed-point numbers*


```solidity
function mulDivRoundDown(uint256 x, uint256 y, uint256 denominator) internal pure returns (uint256 result);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`x`|`uint256`|The multiplicand as an uint256|
|`y`|`uint256`|The multiplier as an uint256|
|`denominator`|`uint256`|The divisor as an uint256|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`result`|`uint256`|The result as an uint256|


### mulDivRoundUp

Calculates ceil(x*y/denominator) with full precision
The result will be rounded up

*Credit to Remco Bloemen under MIT license https://xn--2-umb.com/21/muldiv
Requirements:
- The denominator cannot be zero
- The result must fit within uint256
Caveats:
- This function does not work with fixed-point numbers*


```solidity
function mulDivRoundUp(uint256 x, uint256 y, uint256 denominator) internal pure returns (uint256 result);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`x`|`uint256`|The multiplicand as an uint256|
|`y`|`uint256`|The multiplier as an uint256|
|`denominator`|`uint256`|The divisor as an uint256|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`result`|`uint256`|The result as an uint256|


### mulShiftRoundDown

Calculates floor(x * y / 2**offset) with full precision
The result will be rounded down

*Credit to Remco Bloemen under MIT license https://xn--2-umb.com/21/muldiv
Requirements:
- The offset needs to be strictly lower than 256
- The result must fit within uint256
Caveats:
- This function does not work with fixed-point numbers*


```solidity
function mulShiftRoundDown(uint256 x, uint256 y, uint8 offset) internal pure returns (uint256 result);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`x`|`uint256`|The multiplicand as an uint256|
|`y`|`uint256`|The multiplier as an uint256|
|`offset`|`uint8`|The offset as an uint256, can't be greater than 256|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`result`|`uint256`|The result as an uint256|


### mulShiftRoundUp

Calculates floor(x * y / 2**offset) with full precision
The result will be rounded down

*Credit to Remco Bloemen under MIT license https://xn--2-umb.com/21/muldiv
Requirements:
- The offset needs to be strictly lower than 256
- The result must fit within uint256
Caveats:
- This function does not work with fixed-point numbers*


```solidity
function mulShiftRoundUp(uint256 x, uint256 y, uint8 offset) internal pure returns (uint256 result);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`x`|`uint256`|The multiplicand as an uint256|
|`y`|`uint256`|The multiplier as an uint256|
|`offset`|`uint8`|The offset as an uint256, can't be greater than 256|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`result`|`uint256`|The result as an uint256|


### shiftDivRoundDown

Calculates floor(x << offset / y) with full precision
The result will be rounded down

*Credit to Remco Bloemen under MIT license https://xn--2-umb.com/21/muldiv
Requirements:
- The offset needs to be strictly lower than 256
- The result must fit within uint256
Caveats:
- This function does not work with fixed-point numbers*


```solidity
function shiftDivRoundDown(uint256 x, uint8 offset, uint256 denominator) internal pure returns (uint256 result);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`x`|`uint256`|The multiplicand as an uint256|
|`offset`|`uint8`|The number of bit to shift x as an uint256|
|`denominator`|`uint256`|The divisor as an uint256|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`result`|`uint256`|The result as an uint256|


### shiftDivRoundUp

Calculates ceil(x << offset / y) with full precision
The result will be rounded up

*Credit to Remco Bloemen under MIT license https://xn--2-umb.com/21/muldiv
Requirements:
- The offset needs to be strictly lower than 256
- The result must fit within uint256
Caveats:
- This function does not work with fixed-point numbers*


```solidity
function shiftDivRoundUp(uint256 x, uint8 offset, uint256 denominator) internal pure returns (uint256 result);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`x`|`uint256`|The multiplicand as an uint256|
|`offset`|`uint8`|The number of bit to shift x as an uint256|
|`denominator`|`uint256`|The divisor as an uint256|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`result`|`uint256`|The result as an uint256|


### _getMulProds

Helper function to return the result of `x * y` as 2 uint256


```solidity
function _getMulProds(uint256 x, uint256 y) private pure returns (uint256 prod0, uint256 prod1);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`x`|`uint256`|The multiplicand as an uint256|
|`y`|`uint256`|The multiplier as an uint256|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`prod0`|`uint256`|The least significant 256 bits of the product|
|`prod1`|`uint256`|The most significant 256 bits of the product|


### _getEndOfDivRoundDown

Helper function to return the result of `x * y / denominator` with full precision


```solidity
function _getEndOfDivRoundDown(uint256 x, uint256 y, uint256 denominator, uint256 prod0, uint256 prod1)
    private
    pure
    returns (uint256 result);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`x`|`uint256`|The multiplicand as an uint256|
|`y`|`uint256`|The multiplier as an uint256|
|`denominator`|`uint256`|The divisor as an uint256|
|`prod0`|`uint256`|The least significant 256 bits of the product|
|`prod1`|`uint256`|The most significant 256 bits of the product|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`result`|`uint256`|The result as an uint256|


### sqrt

Calculates the square root of x

*Credit to OpenZeppelin's Math library under MIT license*


```solidity
function sqrt(uint256 x) internal pure returns (uint256 sqrtX);
```

## Errors
### Uint256x256Math__MulShiftOverflow

```solidity
error Uint256x256Math__MulShiftOverflow();
```

### Uint256x256Math__MulDivOverflow

```solidity
error Uint256x256Math__MulDivOverflow();
```

