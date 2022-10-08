---
sidebar_position: 0
sidebar_label: ILBFactory
---

### LBPairInformation

```solidity
struct LBPairInformation {
  uint24 binStep;
  contract ILBPair LBPair;
  bool createdByOwner;
  bool ignoredForRouting;
}
```

### LBPairCreated

```solidity
event LBPairCreated(contract IERC20 tokenX, contract IERC20 tokenY, uint256 binStep, contract ILBPair LBPair, uint256 pid)
```

### FeeRecipientSet

```solidity
event FeeRecipientSet(address oldRecipient, address newRecipient)
```

### FlashLoanFeeSet

```solidity
event FlashLoanFeeSet(uint256 oldFlashLoanFee, uint256 newFlashLoanFee)
```

### FeeParametersSet

```solidity
event FeeParametersSet(address sender, contract ILBPair LBPair, uint256 binStep, uint256 baseFactor, uint256 filterPeriod, uint256 decayPeriod, uint256 reductionFactor, uint256 variableFeeControl, uint256 protocolShare, uint256 maxVolatilityAccumulated)
```

### FactoryLockedStatusUpdated

```solidity
event FactoryLockedStatusUpdated(bool unlocked)
```

### LBPairImplementationSet

```solidity
event LBPairImplementationSet(address oldLBPairImplementation, address LBPairImplementation)
```

### LBPairIgnoredStateChanged

```solidity
event LBPairIgnoredStateChanged(contract ILBPair LBPair, bool ignored)
```

### PresetSet

```solidity
event PresetSet(uint256 binStep, uint256 baseFactor, uint256 filterPeriod, uint256 decayPeriod, uint256 reductionFactor, uint256 variableFeeControl, uint256 protocolShare, uint256 maxVolatilityAccumulated, uint256 sampleLifetime)
```

### PresetRemoved

```solidity
event PresetRemoved(uint256 binStep)
```

### QuoteAssetAdded

```solidity
event QuoteAssetAdded(contract IERC20 quoteAsset)
```

### QuoteAssetRemoved

```solidity
event QuoteAssetRemoved(contract IERC20 quoteAsset)
```

### MAX_FEE

```solidity
function MAX_FEE() external pure returns (uint256)
```

### MIN_BIN_STEP

```solidity
function MIN_BIN_STEP() external pure returns (uint256)
```

### MAX_BIN_STEP

```solidity
function MAX_BIN_STEP() external pure returns (uint256)
```

### MAX_PROTOCOL_SHARE

```solidity
function MAX_PROTOCOL_SHARE() external pure returns (uint256)
```

### LBPairImplementation

```solidity
function LBPairImplementation() external view returns (address)
```

### getNumberOfQuoteAssets

```solidity
function getNumberOfQuoteAssets() external view returns (uint256)
```

### getQuoteAsset

```solidity
function getQuoteAsset(uint256 index) external view returns (contract IERC20)
```

### isQuoteAsset

```solidity
function isQuoteAsset(contract IERC20 token) external view returns (bool)
```

### feeRecipient

```solidity
function feeRecipient() external view returns (address)
```

### flashLoanFee

```solidity
function flashLoanFee() external view returns (uint256)
```

### creationUnlocked

```solidity
function creationUnlocked() external view returns (bool)
```

### allLBPairs

```solidity
function allLBPairs(uint256 id) external returns (contract ILBPair)
```

### getNumberOfLBPairs

```solidity
function getNumberOfLBPairs() external view returns (uint256)
```

### getLBPairInformation

```solidity
function getLBPairInformation(contract IERC20 tokenA, contract IERC20 tokenB, uint256 binStep) external view returns (struct ILBFactory.LBPairInformation)
```

### getPreset

```solidity
function getPreset(uint16 binStep) external view returns (uint256 baseFactor, uint256 filterPeriod, uint256 decayPeriod, uint256 reductionFactor, uint256 variableFeeControl, uint256 protocolShare, uint256 maxAccumulator, uint256 sampleLifetime)
```

### getAllBinSteps

```solidity
function getAllBinSteps() external view returns (uint256[] presetsBinStep)
```

### getAllLBPairs

```solidity
function getAllLBPairs(contract IERC20 tokenX, contract IERC20 tokenY) external view returns (struct ILBFactory.LBPairInformation[] LBPairsBinStep)
```

### setLBPairImplementation

```solidity
function setLBPairImplementation(address LBPairImplementation) external
```

### createLBPair

```solidity
function createLBPair(contract IERC20 tokenX, contract IERC20 tokenY, uint24 activeId, uint16 binStep) external returns (contract ILBPair pair)
```

### setLBPairIgnored

```solidity
function setLBPairIgnored(contract IERC20 tokenX, contract IERC20 tokenY, uint256 binStep, bool ignored) external
```

### setPreset

```solidity
function setPreset(uint16 binStep, uint16 baseFactor, uint16 filterPeriod, uint16 decayPeriod, uint16 reductionFactor, uint24 variableFeeControl, uint16 protocolShare, uint24 maxVolatilityAccumulated, uint16 sampleLifetime) external
```

### removePreset

```solidity
function removePreset(uint16 binStep) external
```

### setFeesParametersOnPair

```solidity
function setFeesParametersOnPair(contract IERC20 tokenX, contract IERC20 tokenY, uint16 binStep, uint16 baseFactor, uint16 filterPeriod, uint16 decayPeriod, uint16 reductionFactor, uint24 variableFeeControl, uint16 protocolShare, uint24 maxVolatilityAccumulated) external
```

### setFeeRecipient

```solidity
function setFeeRecipient(address feeRecipient) external
```

### setFlashLoanFee

```solidity
function setFlashLoanFee(uint256 flashLoanFee) external
```

### setFactoryLockedState

```solidity
function setFactoryLockedState(bool locked) external
```

### addQuoteAsset

```solidity
function addQuoteAsset(contract IERC20 quoteAsset) external
```

### removeQuoteAsset

```solidity
function removeQuoteAsset(contract IERC20 quoteAsset) external
```

### forceDecay

```solidity
function forceDecay(contract ILBPair LBPair) external
```

