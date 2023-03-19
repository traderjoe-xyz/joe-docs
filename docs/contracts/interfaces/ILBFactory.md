## ILBFactory

Required interface of LBFactory contract

### LBPairInformation

```solidity
struct LBPairInformation{
    uint16 binStep;
    ILBPair LBPair;
    bool createdByOwner;
    bool ignoredForRouting;
}
```

Structure to store the LBPair information, such as:
* binStep: The bin step of the LBPair
* LBPair: The address of the LBPair
* createdByOwner: Whether the pair was created by the owner of the factory
* ignoredForRouting: Whether the pair is ignored for routing or not. An ignored pair will not be explored during routes finding

### LBPairCreated

```solidity
event LBPairCreated(
    IERC20 indexed tokenX, 
    IERC20 indexed tokenY, 
    uint256 indexed binStep, 
    ILBPair LBPair, 
    uint256 pid
    )
```

### FeeRecipientSet

```solidity
event FeeRecipientSet(address oldRecipient, address newRecipient)
```

### FlashLoanFeeSet

```solidity
event FlashLoanFeeSet(uint256 oldFlashLoanFee, uint256 newFlashLoanFee)
```

### LBPairImplementationSet

```solidity
event LBPairImplementationSet(address oldLBPairImplementation, address LBPairImplementation)
```

### LBPairIgnoredStateChanged

```solidity
event LBPairIgnoredStateChanged(ILBPair indexed LBPair, bool ignored)
```

### PresetSet

```solidity
event PresetSet(
    uint256 indexed binStep,
    uint256 baseFactor,
    uint256 filterPeriod,
    uint256 decayPeriod,
    uint256 reductionFactor,
    uint256 variableFeeControl,
    uint256 protocolShare,
    uint256 maxVolatilityAccumulator
)
```
### PresetOpenStateChanged

```solidity
event PresetOpenStateChanged(uint256 indexed binStep, bool indexed isOpen)
```

### QuoteAssetAdded

```solidity
event QuoteAssetAdded(IERC20 indexed quoteAsset)
```

### QuoteAssetRemoved

```solidity
event QuoteAssetRemoved(IERC20 indexed quoteAsset)
```

### getMinBinStep

```solidity
function getMinBinStep() external pure override returns (uint256 minBinStep)
```

### getFeeRecipient

```solidity
function getFeeRecipient() external view override returns (address feeRecipient)
```

### getMaxFlashLoanFee

```solidity
function getMaxFlashLoanFee() external pure override returns (uint256 maxFee)
```

### getFlashLoanFee

```solidity
function getFlashLoanFee() external view override returns (uint256 flashloanFee)
```

### getLBPairImplementation

```solidity
function getLBPairImplementation() external view override returns (address lbPairImplementation)
```

### getNumberOfLBPairs

```solidity
function getNumberOfLBPairs() external view override returns (uint256 lbPairNumber)
```

### getLBPairAtIndex

```solidity
function getLBPairAtIndex(uint256 index) external view override returns (ILBPair lbPair)
```

### getNumberOfQuoteAssets

```solidity
function getNumberOfQuoteAssets() external view override returns (uint256 numberOfQuoteAssets)
```

### getQuoteAssetAtIndex

```solidity
function getQuoteAssetAtIndex(uint256 index) external view override returns (IERC20 asset)
```

### isQuoteAsset

```solidity
function isQuoteAsset(IERC20 token) external view override returns (bool isQuote)
```

### getLBPairInformation

```solidity
function getLBPairInformation(IERC20 tokenA, IERC20 tokenB, uint256 binStep) external view override returns (LBPairInformation memory lbPairInformation)
```

### getPreset

```solidity
function getPreset(uint256 binStep) external view override returns (uint256 baseFactor, uint256 filterPeriod, uint256 decayPeriod, uint256 reductionFactor, uint256 variableFeeControl, uint256 protocolShare, uint256 maxVolatilityAccumulator, bool isOpen)
```

### getAllBinSteps

```solidity
function getAllBinSteps() external view override returns (uint256[] memory binStepWithPreset)
```

### getAllLBPairs

```solidity
function getAllLBPairs(IERC20 tokenX, IERC20 tokenY) external view override returns (LBPairInformation[] memory lbPairsAvailable)
```

### setLBPairImplementation

```solidity
function setLBPairImplementation(address newLBPairImplementation) external override onlyOwner
```

### createLBPair

```solidity
function createLBPair(IERC20 tokenX, IERC20 tokenY, uint24 activeId, uint16 binStep) external override returns (ILBPair pair)
```

### setLBPairIgnored

```solidity
function setLBPairIgnored(IERC20 tokenX, IERC20 tokenY, uint16 binStep, bool ignored) external override onlyOwner
```

### setPreset

```solidity
function setPreset(uint16 binStep, uint16 baseFactor, uint16 filterPeriod, uint16 decayPeriod, uint16 reductionFactor, uint24 variableFeeControl, uint16 protocolShare, uint24 maxVolatilityAccumulator, bool isOpen) external override onlyOwner
```

### setPresetOpenState

```solidity
function setPresetOpenState(uint16 binStep, bool isOpen) external override onlyOwner
```

### removePreset

```solidity
function removePreset(uint16 binStep) external override onlyOwner
```

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

### setFeeRecipient

```solidity
function setFeeRecipient(address feeRecipient) external override onlyOwner
```

### setFlashLoanFee

```solidity
function setFlashLoanFee(uint256 flashLoanFee) external override onlyOwner
```

### addQuoteAsset

```solidity
function addQuoteAsset(IERC20 quoteAsset) external override onlyOwner
```

### removeQuoteAsset

```solidity
function removeQuoteAsset(IERC20 quoteAsset) external
```

### forceDecay

```solidity
function forceDecay(ILBPair lbPair) external
```

