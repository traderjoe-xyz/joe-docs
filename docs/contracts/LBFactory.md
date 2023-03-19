## LBFactory

Contract used to deploy and register new LBPairs. Enables setting fee parameters, flashloan fees and LBPair implementation. Unless the `isOpen` is `true`, only the owner of the factory can create pairs.

### getMinBinStep

```solidity
function getMinBinStep() external pure override returns (uint256 minBinStep)
```

Get the minimum bin step a pair can have

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| minBinStep | uint256 | Returns the minimum bin step a pair can have |

### getFeeRecipient

```solidity
function getFeeRecipient() external view override returns (address feeRecipient)
```

Get the protocol fee recipient

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| feeRecipient | address | Returns the protocol fee recipient |

### getMaxFlashLoanFee

```solidity
function getMaxFlashLoanFee() external pure override returns (uint256 maxFee)
```

Get the maximum fee percentage for flashLoans

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| maxFee | uint256 | Returns the maximum fee percentage for flashLoans |

### getFlashLoanFee

```solidity
function getFlashLoanFee() external view override returns (uint256 flashloanFee)
```

Get the fee for flash loans

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| flashloanFee | uint256 | Returns the fee for flash loans |

### getLBPairImplementation

```solidity
function getLBPairImplementation() external view override returns (address lbPairImplementation)
```

Get the address of the LBPair implementation

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| lbPairImplementation | address | Returns the address of the LBPair implementation |

### getNumberOfLBPairs

```solidity
function getNumberOfLBPairs() external view override returns (uint256 lbPairNumber)
```

View function to return the number of LBPairs created

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| lbPairNumber | uint256 | Returns the number of LBPairs created |

### getLBPairAtIndex

```solidity
function getLBPairAtIndex(uint256 index) external view override returns (ILBPair lbPair)
```

View function to return the LBPair created at index `index`

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| index | uint256 | The index |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| lbPair | ILBPair | The address of the LBPair at index `index` |

### getNumberOfQuoteAssets

```solidity
function getNumberOfQuoteAssets() external view override returns (uint256 numberOfQuoteAssets)
```

View function to return the number of quote assets whitelisted

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| numberOfQuoteAssets | uint256 | The number of quote assets |

### getQuoteAssetAtIndex

```solidity
function getQuoteAssetAtIndex(uint256 index) external view override returns (IERC20 asset)
```

View function to return the quote asset whitelisted at index `index`

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| index | uint256 | The index |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| asset | IERC20 | The address of the quoteAsset at index `index` |

### isQuoteAsset

```solidity
function isQuoteAsset(IERC20 token) external view override returns (bool isQuote)
```

View function to return whether a token is a quotedAsset (true) or not (false)

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| token | IERC20 | The address of the asset |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| isQuote | bool | Whether the token is a quote asset or not |

### getLBPairInformation

```solidity
function getLBPairInformation(IERC20 tokenA, IERC20 tokenB, uint256 binStep) external view override returns (LBPairInformation memory lbPairInformation)
```

View function to return the LBPairInformation if it exists, if not, then the address 0 is returned. The order doesn't matter

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| tokenA | IERC20 | The address of the first token of the pair |
| tokenB | IERC20 | The address of the second token of the pair |
| binStep | uint256 | The bin step of the LBPair |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| lbPairInformation | LBPairInformation | The LBPairInformation |

### getPreset

```solidity
function getPreset(uint256 binStep) external view override returns (uint256 baseFactor, uint256 filterPeriod, uint256 decayPeriod, uint256 reductionFactor, uint256 variableFeeControl, uint256 protocolShare, uint256 maxVolatilityAccumulator, bool isOpen)
```

View function to return the different parameters of the preset. Will revert if the preset doesn't exist

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| binStep | uint256 | The bin step of the preset |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| baseFactor | uint256 | The base factor |
| filterPeriod | uint256 | The filter period of the preset |
| decayPeriod | uint256 | The decay period of the preset |
| reductionFactor | uint256 | The reduction factor of the preset |
| variableFeeControl | uint256 | The variable fee control of the preset |
| protocolShare | uint256 | The protocol share of the preset |
| maxVolatilityAccumulator | uint256 | The max volatility accumulator of the preset |
| isOpen | bool | Whether the preset is open or not |

### getAllBinSteps

```solidity
function getAllBinSteps() external view override returns (uint256[] memory binStepWithPreset)
```

View function to return the list of available binStep with a preset

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| binStepWithPreset | uint256[] | The list of binStep |

### getAllLBPairs

```solidity
function getAllLBPairs(IERC20 tokenX, IERC20 tokenY) external view override returns (LBPairInformation[] memory lbPairsAvailable)
```

View function to return all the LBPair of a pair of tokens

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| tokenX | IERC20 | The first token of the pair |
| tokenY | IERC20 | The second token of the pair |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| lbPairsAvailable | LBPairInformation[] | The list of available LBPairs |

### setLBPairImplementation

```solidity
function setLBPairImplementation(address newLBPairImplementation) external override onlyOwner
```

Set the LBPair implementation address

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| newLBPairImplementation | address | The address of the implementation |

### createLBPair

```solidity
function createLBPair(IERC20 tokenX, IERC20 tokenY, uint24 activeId, uint16 binStep) external override returns (ILBPair pair)
```

Create a liquidity bin LBPair for tokenX and tokenY

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| tokenX | IERC20 | The address of the first token |
| tokenY | IERC20 | The address of the second token |
| activeId | uint24 | The active id of the pair |
| binStep | uint16 | The bin step in basis point, used to calculate log(1 + binStep / 10_000) |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| pair | ILBPair | The address of the newly created LBPair |

### setLBPairIgnored

```solidity
function setLBPairIgnored(IERC20 tokenX, IERC20 tokenY, uint16 binStep, bool ignored) external override onlyOwner
```

Function to set whether the pair is ignored or not for routing, it will make the pair unusable by the router

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| tokenX | IERC20 | The address of the first token of the pair |
| tokenY | IERC20 | The address of the second token of the pair |
| binStep | uint16 | The bin step in basis point of the pair |
| ignored | bool | Whether to ignore (true) or not (false) the pair for routing |

### setPreset

```solidity
function setPreset(uint16 binStep, uint16 baseFactor, uint16 filterPeriod, uint16 decayPeriod, uint16 reductionFactor, uint24 variableFeeControl, uint16 protocolShare, uint24 maxVolatilityAccumulator, bool isOpen) external override onlyOwner
```

Sets the preset parameters of a bin step

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| binStep | uint16 | The bin step in basis point, used to calculate the price |
| baseFactor | uint16 | The base factor, used to calculate the base fee, baseFee = baseFactor * binStep |
| filterPeriod | uint16 | The period where the accumulator value is untouched, prevent spam |
| decayPeriod | uint16 | The period where the accumulator value is halved |
| reductionFactor | uint16 | The reduction factor, used to calculate the reduction of the accumulator |
| variableFeeControl | uint24 | The variable fee control, used to control the variable fee, can be 0 to disable it |
| protocolShare | uint16 | The share of the fees received by the protocol |
| maxVolatilityAccumulator | uint24 | The max value of the volatility accumulator |
| isOpen | bool | Whether the preset is open or not |

### setPresetOpenState

```solidity
function setPresetOpenState(uint16 binStep, bool isOpen) external override onlyOwner
```

Sets if the preset is open or not to be used by users

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| binStep | uint16 | The bin step in basis point, used to calculate the price |
| isOpen | bool | Whether the preset is open or not |

### removePreset

```solidity
function removePreset(uint16 binStep) external override onlyOwner
```

Remove the preset linked to a binStep

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| binStep | uint16 | The bin step to remove |

### setFeesParametersOnPair

```solidity
function setFeesParametersOnPair(
    IERC20 tokenX,
    IERC20 tokenY,
    uint16 binStep,
    uint16 baseFactor,
    uint16 filterPeriod,
    uint16 decayPeriod,
    uint16 reductionFactor,
    uint24 variableFeeControl,
    uint16 protocolShare,
    uint24 maxVolatilityAccumulator
) external override onlyOwner
```

Function to set the fee parameter of a LBPair.

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| tokenX | IERC20 | The address of the first token |
| tokenY | IERC20 | The address of the second token |
| binStep | uint16 | The bin step in basis point, used to calculate the price |
| baseFactor | uint16 | The base factor, used to calculate the base fee, baseFee = baseFactor * binStep |
| filterPeriod | uint16 | The period where the accumulator value is untouched, prevent spam |
| decayPeriod | uint16 | The period where the accumulator value is halved |
| reductionFactor | uint16 | The reduction factor, used to calculate the reduction of the accumulator |
| variableFeeControl | uint24 | The variable fee control, used to control the variable fee, can be 0 to disable it |
| protocolShare | uint16 | The share of the fees received by the protocol |
| maxVolatilityAccumulator | uint24 | The max value of volatility accumulator |

### setFeeRecipient

```solidity
function setFeeRecipient(address feeRecipient) external override onlyOwner
```

Function to set the recipient of the fees. This address needs to be able to receive ERC20s.

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| feeRecipient | address | The address of the recipient |

### setFlashLoanFee

```solidity
function setFlashLoanFee(uint256 flashLoanFee) external override onlyOwner
```

Function to set the flash loan fee.

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| flashLoanFee | uint256 | The value of the fee for flash loan |

### addQuoteAsset

```solidity
function addQuoteAsset(IERC20 quoteAsset) external override onlyOwner
```

Function to add an asset to the whitelist of quote assets.

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| quoteAsset | IERC20 | The quote asset (e.g: NATIVE, USDC...) |

### removeQuoteAsset

```solidity
function removeQuoteAsset(IERC20 quoteAsset) external override onlyOwner
```

Function to remove an asset from the whitelist of quote assets.

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| quoteAsset | IERC20 | The quote asset (e.g: NATIVE, USDC...) |

### forceDecay

```solidity
function forceDecay(ILBPair pair) external override onlyOwner
```

Force Decay.

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| pair | ILBPair | The address of the LBPairs |

### _setFeeRecipient

```solidity
function _setFeeRecipient(address feeRecipient) internal
```

Internal function to set the recipient of the fee.

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| feeRecipient | address | The address of the recipient |

### _getLBPairInformation

```solidity
function _getLBPairInformation(IERC20 tokenA, IERC20 tokenB, uint256 binStep) internal view returns (LBPairInformation memory)
```

Returns the LBPairInformation if it exists, if not, then the address 0 is returned. The order doesn't matter.

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| tokenA | IERC20 | The address of the first token of the pair |
| tokenB | IERC20 | The address of the second token of the pair |
| binStep | uint256 | The bin step of the LBPair |

### _sortTokens

```solidity
function _sortTokens(IERC20 tokenA, IERC20 tokenB) private pure returns (IERC20, IERC20)
```

Private view function to sort 2 tokens in ascending order.

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| tokenA | IERC20 | The first token |
| tokenB | IERC20 | The second token |
