## Uint128x128 Math

Helper contract used for power and log calculations

### log2

```solidity
function log2(uint256 x) internal pure returns (int256 result)
```

Calculates the binary logarithm of x. Based on the iterative approximation algorithm. Requirements: - x must be greater than zero. Caveats: - The results are not perfectly accurate to the last decimal, due to the lossy precision of the iterative approximation. Also because x is converted to an unsigned 129.127-binary fixed-point number during the operation to optimize the multiplication.

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| x | uint256 | The unsigned 128.128-binary fixed-point number for which to calculate the binary logarithm. |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| result | int256 | The binary logarithm as a signed 128.128-binary fixed-point number. |

### pow

```solidity
function pow(uint256 x, int256 y) internal pure returns (uint256 result)
```

Returns the value of x^y. It calculates `1 / x^abs(y)` if x is bigger than 2^128. At the end of the operations, we invert the result if needed.

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| x | uint256 | The unsigned 128.128-binary fixed-point number for which to calculate the power |
| y | int256 | A relative number without any decimals, needs to be between ]2^21; 2^21[ |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| result | uint256 | The value of x^y. It calculates `1 / x^abs(y)` if x is bigger than 2^128. At the end of the operations, we invert the result if needed. |