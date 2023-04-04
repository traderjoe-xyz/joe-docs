## LBPair

The Liquidity Book Pair contract is the core contract of the Liquidity Book protocol

### initialize

```solidity
function initialize(
    uint16 baseFactor,
    uint16 filterPeriod,
    uint16 decayPeriod,
    uint16 reductionFactor,
    uint24 variableFeeControl,
    uint16 protocolShare,
    uint24 maxVolatilityAccumulator,
    uint24 activeId
) external override onlyFactory
```

Initialize the Liquidity Book Pair fee parameters and active id. Can only be called by the Liquidity Book Factory.

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| baseFactor | uint16 | The base factor for the static fee |
| filterPeriod | uint16 | The filter period for the static fee |
| decayPeriod | uint16 | The decay period for the static fee |
| reductionFactor | uint16 | The reduction factor for the static fee |
| variableFeeControl | uint24 | The variable fee control for the static fee |
| protocolShare | uint16 | The protocol share for the static fee |
| maxVolatilityAccumulator | uint24 | The max volatility accumulator for the static fee |
| activeId | uint24 | The active id of the Liquidity Book Pair |

### getFactory

```solidity
function getFactory() external view override returns (ILBFactory factory)
```

Returns the Liquidity Book Factory.

### getTokenX

```solidity
function getTokenX() external pure override returns (IERC20 tokenX)
```

Returns the token X of the Liquidity Book Pair.

### getTokenY

```solidity
function getTokenY() external pure override returns (IERC20 tokenY)
```

Returns the token Y of the Liquidity Book Pair.

### getBinStep

```solidity
function getBinStep() external pure override returns (uint16)
```

Returns the bin step of the Liquidity Book Pair.

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
|   | uint16 | The bin step of the Liquidity Book Pair, in 10_000th |

### getReserves

```solidity
function getReserves() external view override returns (uint128 reserveX, uint128 reserveY)
```

Returns the reserves of the Liquidity Book Pair.

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| reserveX  | uint128 | The reserve of token X |
| reserveY  | uint128 | The reserve of token Y |

### getActiveId

```solidity
function getActiveId() external view override returns (uint24 activeId)
```

Returns the active id of the Liquidity Book Pair.

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| activeId | uint24 | The active id of the Liquidity Book Pair |

### getBin

```solidity
function getBin(uint24 id) external view override returns (uint128 binReserveX, uint128 binReserveY)
```

Returns the reserves of a bin.

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| id  | uint24 | The id of the bin |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| binReserveX | uint128 | The reserve of token X in the bin |
| binReserveY  | uint128 | The reserve of token Y in the bin |

### getNextNonEmptyBin

```solidity
function getNextNonEmptyBin(bool swapForY, uint24 id) external view override returns (uint24 nextId)
```

Returns the next non-empty bin.

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| swapForY | bool | Whether the swap is for token Y (true) or token X (false) |
| id | uint24 | The id of the bin |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| nextId | uint24 | The id of the next non-empty bin |

### getProtocolFees

```solidity
function getProtocolFees() external view returns (uint128 protocolFeeX, uint128 protocolFeeY)
```

Returns the protocol fees of the Liquidity Book Pair

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| protocolFeeX | uint128 | The protocol fees of token X |
| protocolFeeY | uint128 | The protocol fees of token Y |

### getStaticFeeParameters

```solidity
function getStaticFeeParameters() external view returns (uint16 baseFactor, uint16 filterPeriod, uint16 decayPeriod, uint16 reductionFactor, uint24 variableFeeControl, uint16 protocolShare, uint24 maxVolatilityAccumulator)
```

Returns the static fee parameters of the Liquidity Book Pair

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| baseFactor | uint16 | The base factor for the static fee |
| filterPeriod | uint16 | The filter period for the static fee |
| decayPeriod | uint16 | The decay period for the static fee |
| reductionFactor | uint16 | The reduction factor for the static fee |
| variableFeeControl | uint24 | The variable fee control for the static fee |
| protocolShare | uint16 | The protocol share for the static fee |
| maxVolatilityAccumulator | uint24 | The maximum volatility accumulator for the static fee |

### getVariableFeeParameters

```solidity
function getVariableFeeParameters() external view returns (uint24 volatilityAccumulator, uint24 volatilityReference, uint24 idReference, uint40 timeOfLastUpdate)
```

Returns the variable fee parameters of the Liquidity Book Pair

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| volatilityAccumulator | uint24 | The volatility accumulator for the variable fee |
| volatilityReference | uint24 | The volatility reference for the variable fee |
| idReference | uint24 | The id reference for the variable fee |
| timeOfLastUpdate | uint40 | The time of last update for the variable fee |

### getOracleParameters

```solidity
function getOracleParameters() external view returns (uint8 sampleLifetime, uint16 size, uint16 activeSize, uint40 lastUpdated, uint40 firstTimestamp)
```

Returns the oracle parameters of the Liquidity Book Pair

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| sampleLifetime | uint8 | The sample lifetime for the oracle |
| size | uint16 | The size of the oracle |
| activeSize | uint16 | The active size of the oracle |
| lastUpdated | uint40 | The last updated timestamp of the oracle |
| firstTimestamp | uint40 | The first timestamp of the oracle, i.e. the timestamp of the oldest sample |

### getOracleSampleAt

```solidity
function getOracleSampleAt(uint40 lookupTimestamp) external view returns (uint64 cumulativeId, uint64 cumulativeVolatility, uint64 cumulativeBinCrossed)
```

Returns the cumulative values of the Liquidity Book Pair at a given timestamp

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| lookupTimestamp | uint40 | The timestamp at which to look up the cumulative values |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| cumulativeId | uint64 | The cumulative id of the Liquidity Book Pair at the given timestamp |
| cumulativeVolatility | uint64 | The cumulative volatility of the Liquidity Book Pair at the given timestamp |
| cumulativeBinCrossed | uint64 | The cumulative bin crossed of the Liquidity Book Pair at the given timestamp |

### getPriceFromId

```solidity
function getPriceFromId(uint24 id) external pure returns (uint256 price)
```

Returns the price corresponding to the given id, as a 128.128-binary fixed-point number

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| id | uint24 | The id of the bin |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| price | uint256 | The price corresponding to this id |

### getIdFromPrice

```solidity
function getIdFromPrice(uint256 price) external pure returns (uint24 id)
```

Returns the id corresponding to the given price

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| price | uint256 | The price of y per x as a 128.128-binary fixed-point number |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| id | uint24 | The id of the bin corresponding to this price |

### getSwapIn

```solidity
function getSwapIn(uint128 amountOut, bool swapForY) external view returns (uint128 amountIn, uint128 amountOutLeft, uint128 fee)
```

Simulates a swap in.

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| amountOut | uint128 | The amount of token X or Y to swap in |
| swapForY | bool | Whether the swap is for token Y (true) or token X (false) |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| amountIn | uint128 | The amount of token X or Y that can be swapped in, including the fee |
| amountOutLeft | uint128 | The amount of token Y or X that cannot be swapped out |
| fee | uint128 | The fee of the swap |

### getSwapOut

```solidity
function getSwapOut(uint128 amountIn, bool swapForY) external view override returns (uint128 amountInLeft, uint128 amountOut, uint128 fee)
```

Simulates a swap out.
If `amountInLeft` is greater than zero, the swap out is not possible,
and the maximum amount that can be swapped is `amountIn - amountInLeft` for `amountOut`.

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| amountIn | uint128 | The amount of token X or Y to swap in |
| swapForY | bool | Whether the swap is for token Y (true) or token X (false) |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| amountInLeft | uint128 | The amount of token X or Y that cannot be swapped in |
| amountOut | uint128 | The amount of token Y or X that can be swapped out |
| fee | uint128 | The fee of the swap |

### swap

```solidity
function swap(bool swapForY, address to) external override nonReentrant returns (bytes32 amountsOut)
```

Swap tokens iterating over the bins until the entire amount is swapped.
Token X will be swapped for token Y if `swapForY` is true, and token Y for token X if `swapForY` is false.
This function will not transfer the tokens from the caller, it is expected that the tokens have already been
transferred to this contract through another contract, most likely the router.
That is why this function shouldn't be called directly, but only through one of the swap functions of a router
that will also perform safety checks, such as minimum amounts and slippage.
The variable fee is updated throughout the swap, it increases with the number of bins crossed.
The oracle is updated at the end of the swap.

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| swapForY | bool | Whether you're swapping token X for token Y (true) or token Y for token X (false) |
| to | address | The address to send the tokens to |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| amountsOut | bytes32 | The encoded amounts of token X and token Y sent to `to` |

### flashLoan

```solidity
function flashLoan(ILBFlashLoanCallback receiver, bytes32 amounts, bytes calldata data) external override nonReentrant
```

Flash loan tokens from the pool to a receiver contract and execute a callback function.
The receiver contract is expected to return the tokens plus a fee to this contract.
The fee is calculated as a percentage of the amount borrowed, and is the same for both tokens.

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| receiver | ILBFlashLoanCallback | The contract that will receive the tokens and execute the callback function |
| amounts | bytes32 | The encoded amounts of token X and token Y to flash loan |
| data | bytes | Any data that will be passed to the callback function |

### mint

```solidity
function mint(address to, bytes32[] calldata liquidityConfigs, address refundTo) external override nonReentrant returns (bytes32 amountsReceived, bytes32 amountsLeft, uint256[] memory liquidityMinted)
```

Mint liquidity tokens by depositing tokens into the pool.
It will mint Liquidity Book (LB) tokens for each bin where the user adds liquidity.
This function will not transfer the tokens from the caller, it is expected that the tokens have already been
transferred to this contract through another contract, most likely the router.
That is why this function shouldn't be called directly, but through one of the add liquidity functions of a
router that will also perform safety checks.
Any excess amount of token will be sent to the `to` address.

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| to | address | The address that will receive the LB tokens |
| liquidityConfigs | bytes32[] | The encoded liquidity configurations, each one containing the id of the bin and the percentage of token X and token Y to add to the bin. |
| refundTo | address | The address that will receive the excess amount of tokens |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| amountsReceived | bytes32 | The amounts of token X and token Y received by the pool |
| amountsLeft | bytes32 | The amounts of token X and token Y that were not added to the pool and were sent to `to` |
| liquidityMinted | uint256[] | The amounts of LB tokens minted for each bin |

### burn

```solidity
function burn(address from, address to, uint256[] calldata ids, uint256[] calldata amountsToBurn) external override nonReentrant checkApproval(from, msg.sender) returns (bytes32[] memory amounts)
```

Burn Liquidity Book (LB) tokens and withdraw tokens from the pool. This function will burn the tokens directly from the caller

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| from | address | The address that will burn the LB tokens |
| to | address | The address that will receive the tokens |
| ids | uint256[] | The ids of the bins from which to withdraw |
| amountsToBurn | uint256[] | The amounts of LB tokens to burn for each bin |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| amounts | bytes32[] | The amounts of token X and token Y received by the user |

### collectProtocolFees

```solidity
function collectProtocolFees() external override nonReentrant onlyProtocolFeeRecipient returns (bytes32 collectedProtocolFees)
```

Collect the protocol fees from the pool.

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| collectedProtocolFees | bytes32 | The amount of protocol fees collected |

### increaseOracleLength

```solidity
function increaseOracleLength(uint16 newLength) external override
```

Increase the length of the oracle used by the pool

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| newLength | uint16 | The new length of the oracle |

### setStaticFeeParameters

```solidity
function setStaticFeeParameters(
    uint16 baseFactor,
    uint16 filterPeriod,
    uint16 decayPeriod,
    uint16 reductionFactor,
    uint24 variableFeeControl,
    uint16 protocolShare,
    uint24 maxVolatilityAccumulator
) external override onlyFactory
```

Sets the static fee parameters of the pool

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| baseFactor | uint16 | The base factor of the static fee |
| filterPeriod | uint16 | The filter period of the static fee |
| decayPeriod | uint16 | The decay period of the static fee |
| reductionFactor | uint16 | The reduction factor of the static fee |
| variableFeeControl | uint24 | The variable fee control of the static fee |
| protocolShare | uint16 | The protocol share of the static fee |
| maxVolatilityAccumulator | uint24 | The max volatility accumulator of the static fee |

### forceDecay

```solidity
function forceDecay() external override onlyFactory
```

Forces the decay of the volatility reference variables

### _tokenX

```solidity
function _tokenX() internal pure returns (IERC20)
```

Returns the address of the token X

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
|  | IERC20 | The address of the token X |

### _tokenY

```solidity
function _tokenY() internal pure returns (IERC20)
```

Returns the address of the token Y

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
|  | IERC20 | The address of the token Y |

### _binStep

```solidity
function _binStep() internal pure returns (uint16)
```

Returns the bin step of the pool, in basis points

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
|  | uint16 | The bin step of the pool |

### _getNextNonEmptyBin

```solidity
function _getNextNonEmptyBin(bool swapForY, uint24 id) internal view returns (uint24)
```

Returns next non-empty bin

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| swapForY | bool | Whether the swap is for Y |
| id | uint24 | The id of the bin |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
|  | uint24 | The id of the next non-empty bin |

### _getFlashLoanFees

```solidity
function _getFlashLoanFees(bytes32 amounts) private view returns (bytes32)
```

Returns the encoded fees amounts for a flash loan

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| amounts | bytes32 | The amounts of the flash loan |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
|  | bytes32 | The encoded fees amounts |

### _setStaticFeeParameters

```solidity
function _setStaticFeeParameters(bytes32 parameters, uint16 baseFactor, uint16 filterPeriod, uint16 decayPeriod, uint16 reductionFactor, uint24 variableFeeControl, uint16 protocolShare, uint24 maxVolatilityAccumulator) internal
```

Sets the static fee parameters of the pair

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| parameters | bytes32 | The current parameters of the pair |
| baseFactor | uint16 | The base factor of the static fee |
| filterPeriod | uint16 | The filter period of the static fee |
| decayPeriod | uint16 | The decay period of the static fee |
| reductionFactor | uint16 | The reduction factor of the static fee |
| variableFeeControl | uint24 | The variable fee control of the static fee |
| protocolShare | uint16 | The protocol share of the static fee |
| maxVolatilityAccumulator | uint24 | The max volatility accumulator of the static fee |

### _mintBin

```solidity
function _mintBin(uint24 activeId, uint24 id, bytes32 maxAmountsInToBin, bytes32 parameters) internal returns (uint256 shares, bytes32 amountsIn, bytes32 amountsInToBin)
```

Helper function to mint liquidity in a bin

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| activeId | uint24 | The id of the active bin |
| id | uint24 | The id of the bin |
| maxAmountsInToBin | bytes32 | The maximum amounts in to the bin |
| parameters | bytes32 | The parameters of the pair |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| shares | uint256 | The amount of shares minted |
| amountsIn | bytes32 | The amounts in |
| amountsInToBin | bytes32 | The amounts in to the bin |