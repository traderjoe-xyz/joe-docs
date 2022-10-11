---
sidebar_position: 0
sidebar_label: LBFactory
---

## LBFactory

Contract used to deploy and register new LBPairs.
Enables setting fee parameters, flashloan fees and LBPair implementation.
Unless the `creationUnlocked` is `true`, only the owner of the factory can create pairs.

### constructor

```solidity
constructor(address _feeRecipient, uint256 _flashLoanFee) public
```

Constructor

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _feeRecipient | address | The address of the fee recipient |
| _flashLoanFee | uint256 | The value of the fee for flash loan |

### getNumberOfLBPairs

```solidity
function getNumberOfLBPairs() external view override returns (uint256)
```

View function to return the number of LBPairs created

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| [0] | uint256 | The number of LBPair |

### getNumberOfQuoteAssets

```solidity
function getNumberOfQuoteAssets() external view override returns (uint256)
```

View function to return the number of quote assets whitelisted

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| [0] | uint256 | The number of quote assets |

### getQuoteAsset

```solidity
function getQuoteAsset(uint256 _index) external view override returns (contract IERC20)
```

View function to return the quote asset whitelisted at index `index`

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _index | uint256 | The index |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| [0] | contract IERC20 | The address of the _quoteAsset at index `index` |

### isQuoteAsset

```solidity
function isQuoteAsset(contract IERC20 _token) external view override returns (bool)
```

View function to return whether a token is a quotedAsset (true) or not (false)

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _token | contract IERC20 | The address of the asset |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| [0] | bool | Whether the token is a quote asset or not |

### getLBPairInformation

```solidity
function getLBPairInformation(contract IERC20 _tokenA, contract IERC20 _tokenB, uint256 _binStep) external view override returns (struct ILBFactory.LBPairInformation)
```

Returns the LBPairInformation if it exists,
if not, then the address 0 is returned. The order doesn't matter

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _tokenA | contract IERC20 | The address of the first token of the pair |
| _tokenB | contract IERC20 | The address of the second token of the pair |
| _binStep | uint256 | The bin step of the LBPair |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| [0] | struct ILBFactory.LBPairInformation | The LBPairInformation |

### getPreset

```solidity
function getPreset(uint16 _binStep) external view override returns (uint256 baseFactor, uint256 filterPeriod, uint256 decayPeriod, uint256 reductionFactor, uint256 variableFeeControl, uint256 protocolShare, uint256 maxVolatilityAccumulated, uint256 sampleLifetime)
```

View function to return the different parameters of the preset

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _binStep | uint16 | The bin step of the preset |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| baseFactor | uint256 | The base factor |
| filterPeriod | uint256 | The filter period of the preset |
| decayPeriod | uint256 | The decay period of the preset |
| reductionFactor | uint256 | The reduction factor of the preset |
| variableFeeControl | uint256 | The variable fee control of the preset |
| protocolShare | uint256 | The protocol share of the preset |
| maxVolatilityAccumulated | uint256 | The max volatility accumulated of the preset |
| sampleLifetime | uint256 | The sample lifetime of the preset |

### getAllBinSteps

```solidity
function getAllBinSteps() external view override returns (uint256[] presetsBinStep)
```

View function to return the list of available binStep with a preset

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| presetsBinStep | uint256[] | The list of binStep |

### getAllLBPairs

```solidity
function getAllLBPairs(contract IERC20 _tokenX, contract IERC20 _tokenY) external view override returns (struct ILBFactory.LBPairInformation[] LBPairsAvailable)
```

View function to return all the LBPair of a pair of tokens

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _tokenX | contract IERC20 | The first token of the pair |
| _tokenY | contract IERC20 | The second token of the pair |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| LBPairsAvailable | struct ILBFactory.LBPairInformation[] | The list of available LBPairs |

### setLBPairImplementation

```solidity
function setLBPairImplementation(address _LBPairImplementation) external override onlyOwner
```

Set the LBPair implementation address

_Needs to be called by the owner_

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _LBPairImplementation | address | The address of the implementation |

### createLBPair

```solidity
function createLBPair(contract IERC20 _tokenX, contract IERC20 _tokenY, uint24 _activeId, uint16 _binStep) external override returns (contract ILBPair _LBPair)
```

Create a liquidity bin LBPair for _tokenX and _tokenY

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _tokenX | contract IERC20 | The address of the first token |
| _tokenY | contract IERC20 | The address of the second token |
| _activeId | uint24 | The active id of the pair |
| _binStep | uint16 | The bin step in basis point, used to calculate log(1 + binStep) |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| _LBPair | contract ILBPair | The address of the newly created LBPair |

### setLBPairIgnored

```solidity
function setLBPairIgnored(contract IERC20 _tokenX, contract IERC20 _tokenY, uint256 _binStep, bool _ignored) external override onlyOwner 
```

Function to set whether the pair is ignored or not for routing, it will make the pair unusable by the router

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _tokenX | contract IERC20 | The address of the first token of the pair |
| _tokenY | contract IERC20 | The address of the second token of the pair |
| _binStep | uint256 | The bin step in basis point of the pair |
| _ignored | bool | Whether to ignore (true) or not (false) the pair for routing |

### setPreset

```solidity
function setPreset(uint16 _binStep, uint16 _baseFactor, uint16 _filterPeriod, uint16 _decayPeriod, uint16 _reductionFactor, uint24 _variableFeeControl, uint16 _protocolShare, uint24 _maxVolatilityAccumulated, uint16 _sampleLifetime) external override onlyOwner
```

Sets the preset parameters of a bin step

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _binStep | uint16 | The bin step in basis point, used to calculate log(1 + binStep) |
| _baseFactor | uint16 | The base factor, used to calculate the base fee, baseFee = baseFactor * binStep |
| _filterPeriod | uint16 | The period where the accumulator value is untouched, prevent spam |
| _decayPeriod | uint16 | The period where the accumulator value is halved |
| _reductionFactor | uint16 | The reduction factor, used to calculate the reduction of the accumulator |
| _variableFeeControl | uint24 | The variable fee control, used to control the variable fee, can be 0 to disable them |
| _protocolShare | uint16 | The share of the fees received by the protocol |
| _maxVolatilityAccumulated | uint24 | The max value of the volatility accumulated |
| _sampleLifetime | uint16 | The lifetime of an oracle's sample |

### removePreset

```solidity
function removePreset(uint16 _binStep) external override onlyOwner
```

Remove the preset linked to a binStep

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _binStep | uint16 | The bin step to remove |

### setFeesParametersOnPair

```solidity
function setFeesParametersOnPair(contract IERC20 _tokenX, contract IERC20 _tokenY, uint16 _binStep, uint16 _baseFactor, uint16 _filterPeriod, uint16 _decayPeriod, uint16 _reductionFactor, uint24 _variableFeeControl, uint16 _protocolShare, uint24 _maxVolatilityAccumulated) external override onlyOwner
```

Function to set the fee parameter of a LBPair

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _tokenX | contract IERC20 | The address of the first token |
| _tokenY | contract IERC20 | The address of the second token |
| _binStep | uint16 | The bin step in basis point, used to calculate log(1 + binStep) |
| _baseFactor | uint16 | The base factor, used to calculate the base fee, baseFee = baseFactor * binStep |
| _filterPeriod | uint16 | The period where the accumulator value is untouched, prevent spam |
| _decayPeriod | uint16 | The period where the accumulator value is halved |
| _reductionFactor | uint16 | The reduction factor, used to calculate the reduction of the accumulator |
| _variableFeeControl | uint24 | The variable fee control, used to control the variable fee, can be 0 to disable them |
| _protocolShare | uint16 | The share of the fees received by the protocol |
| _maxVolatilityAccumulated | uint24 | The max value of volatility accumulated |

### setFeeRecipient

```solidity
function setFeeRecipient(address _feeRecipient) external override onlyOwner
```

Function to set the recipient of the fees. This address needs to be able to receive ERC20s

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _feeRecipient | address | The address of the recipient |

### setFlashLoanFee

```solidity
function setFlashLoanFee(uint256 _flashLoanFee) external override onlyOwner
```

Function to set the flash loan fee

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _flashLoanFee | uint256 | The value of the fee for flash loan |

### setFactoryLockedState

```solidity
function setFactoryLockedState(bool _locked) external override onlyOwner
```

Function to set the creation restriction of the Factory

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _locked | bool | If the creation is restricted (true) or not (false) |

### addQuoteAsset

```solidity
function addQuoteAsset(contract IERC20 _quoteAsset) external override onlyOwner
```

Function to add an asset to the whitelist of quote assets

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _quoteAsset | contract IERC20 | The quote asset (e.g: AVAX, USDC...) |

### removeQuoteAsset

```solidity
function removeQuoteAsset(contract IERC20 _quoteAsset) external override onlyOwner
```

Function to remove an asset to the whitelist of quote assets

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _quoteAsset | contract IERC20 | The quote asset (e.g: AVAX, USDC...) |

### _setFeeRecipient

```solidity
function _setFeeRecipient(address _feeRecipient) internal
```

Internal function to set the recipient of the fee

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _feeRecipient | address | The address of the recipient |

### forceDecay

```solidity
function forceDecay(contract ILBPair _LBPair) external override onlyOwner
```
