# LBFactory
[Git Source](https://github.com/traderjoe-xyz/joe-v2/blob/16f011d25e6bf6d0a0c479974345b623d491104f/src/LBFactory.sol)

**Inherits:**
Ownable2Step, AccessControl, [ILBFactory](/src/interfaces/ILBFactory.sol/interface.ILBFactory.md)

**Author:**
Trader Joe

Contract used to deploy and register new LBPairs.
Enables setting fee parameters, flashloan fees and LBPair implementation.
Unless the `isOpen` is `true`, only the owner of the factory can create pairs.


## State Variables
### LB_HOOKS_MANAGER_ROLE

```solidity
bytes32 public constant LB_HOOKS_MANAGER_ROLE = keccak256("LB_HOOKS_MANAGER_ROLE");
```


### _OFFSET_IS_PRESET_OPEN

```solidity
uint256 private constant _OFFSET_IS_PRESET_OPEN = 255;
```


### _MIN_BIN_STEP

```solidity
uint256 private constant _MIN_BIN_STEP = 1;
```


### _MAX_FLASHLOAN_FEE

```solidity
uint256 private constant _MAX_FLASHLOAN_FEE = 0.1e18;
```


### _feeRecipient

```solidity
address private _feeRecipient;
```


### _flashLoanFee

```solidity
uint256 private _flashLoanFee;
```


### _lbPairImplementation

```solidity
address private _lbPairImplementation;
```


### _allLBPairs

```solidity
ILBPair[] private _allLBPairs;
```


### _lbPairsInfo
*Mapping from a (tokenA, tokenB, binStep) to a LBPair. The tokens are ordered to save gas, but they can be
in the reverse order in the actual pair.
Always query one of the 2 tokens of the pair to assert the order of the 2 tokens*


```solidity
mapping(IERC20 => mapping(IERC20 => mapping(uint256 => LBPairInformation))) private _lbPairsInfo;
```


### _presets

```solidity
EnumerableMap.UintToUintMap private _presets;
```


### _quoteAssetWhitelist

```solidity
EnumerableSet.AddressSet private _quoteAssetWhitelist;
```


### _availableLBPairBinSteps
*Mapping from a (tokenA, tokenB) to a set of available bin steps, this is used to keep track of the
bin steps that are already used for a pair.
The tokens are ordered to save gas, but they can be in the reverse order in the actual pair.
Always query one of the 2 tokens of the pair to assert the order of the 2 tokens*


```solidity
mapping(IERC20 => mapping(IERC20 => EnumerableSet.UintSet)) private _availableLBPairBinSteps;
```


## Functions
### constructor

Constructor


```solidity
constructor(address feeRecipient, address initialOwner, uint256 flashLoanFee) Ownable(initialOwner);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`feeRecipient`|`address`|The address of the fee recipient|
|`initialOwner`|`address`||
|`flashLoanFee`|`uint256`|The value of the fee for flash loan|


### getMinBinStep

Get the minimum bin step a pair can have


```solidity
function getMinBinStep() external pure override returns (uint256 minBinStep);
```
**Returns**

|Name|Type|Description|
|----|----|-----------|
|`minBinStep`|`uint256`|minBinStep|


### getFeeRecipient

Get the protocol fee recipient


```solidity
function getFeeRecipient() external view override returns (address feeRecipient);
```
**Returns**

|Name|Type|Description|
|----|----|-----------|
|`feeRecipient`|`address`|feeRecipient|


### getMaxFlashLoanFee

Get the maximum fee percentage for flashLoans


```solidity
function getMaxFlashLoanFee() external pure override returns (uint256 maxFee);
```
**Returns**

|Name|Type|Description|
|----|----|-----------|
|`maxFee`|`uint256`|maxFee|


### getFlashLoanFee

Get the fee for flash loans, in 1e18


```solidity
function getFlashLoanFee() external view override returns (uint256 flashLoanFee);
```
**Returns**

|Name|Type|Description|
|----|----|-----------|
|`flashLoanFee`|`uint256`|The fee for flash loans, in 1e18|


### getLBPairImplementation

Get the address of the LBPair implementation


```solidity
function getLBPairImplementation() external view override returns (address lbPairImplementation);
```
**Returns**

|Name|Type|Description|
|----|----|-----------|
|`lbPairImplementation`|`address`|The address of the LBPair implementation|


### getNumberOfLBPairs

View function to return the number of LBPairs created


```solidity
function getNumberOfLBPairs() external view override returns (uint256 lbPairNumber);
```
**Returns**

|Name|Type|Description|
|----|----|-----------|
|`lbPairNumber`|`uint256`|lbPairNumber|


### getLBPairAtIndex

View function to return the LBPair created at index `index`


```solidity
function getLBPairAtIndex(uint256 index) external view override returns (ILBPair lbPair);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`index`|`uint256`|The index|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`lbPair`|`ILBPair`|The address of the LBPair at index `index`|


### getNumberOfQuoteAssets

View function to return the number of quote assets whitelisted


```solidity
function getNumberOfQuoteAssets() external view override returns (uint256 numberOfQuoteAssets);
```
**Returns**

|Name|Type|Description|
|----|----|-----------|
|`numberOfQuoteAssets`|`uint256`|The number of quote assets|


### getQuoteAssetAtIndex

View function to return the quote asset whitelisted at index `index`


```solidity
function getQuoteAssetAtIndex(uint256 index) external view override returns (IERC20 asset);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`index`|`uint256`|The index|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`asset`|`IERC20`|The address of the quoteAsset at index `index`|


### isQuoteAsset

View function to return whether a token is a quotedAsset (true) or not (false)


```solidity
function isQuoteAsset(IERC20 token) external view override returns (bool isQuote);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`token`|`IERC20`|The address of the asset|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`isQuote`|`bool`|Whether the token is a quote asset or not|


### getLBPairInformation

Returns the LBPairInformation if it exists,
if not, then the address 0 is returned. The order doesn't matter


```solidity
function getLBPairInformation(IERC20 tokenA, IERC20 tokenB, uint256 binStep)
    external
    view
    override
    returns (LBPairInformation memory lbPairInformation);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`tokenA`|`IERC20`|The address of the first token of the pair|
|`tokenB`|`IERC20`|The address of the second token of the pair|
|`binStep`|`uint256`|The bin step of the LBPair|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`lbPairInformation`|`LBPairInformation`|The LBPairInformation|


### getPreset

View function to return the different parameters of the preset
Will revert if the preset doesn't exist


```solidity
function getPreset(uint256 binStep)
    external
    view
    override
    returns (
        uint256 baseFactor,
        uint256 filterPeriod,
        uint256 decayPeriod,
        uint256 reductionFactor,
        uint256 variableFeeControl,
        uint256 protocolShare,
        uint256 maxVolatilityAccumulator,
        bool isOpen
    );
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`binStep`|`uint256`|The bin step of the preset|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`baseFactor`|`uint256`|The base factor|
|`filterPeriod`|`uint256`|The filter period of the preset|
|`decayPeriod`|`uint256`|The decay period of the preset|
|`reductionFactor`|`uint256`|The reduction factor of the preset|
|`variableFeeControl`|`uint256`|The variable fee control of the preset|
|`protocolShare`|`uint256`|The protocol share of the preset|
|`maxVolatilityAccumulator`|`uint256`|The max volatility accumulator of the preset|
|`isOpen`|`bool`|Whether the preset is open or not|


### getAllBinSteps

View function to return the list of available binStep with a preset


```solidity
function getAllBinSteps() external view override returns (uint256[] memory binStepWithPreset);
```
**Returns**

|Name|Type|Description|
|----|----|-----------|
|`binStepWithPreset`|`uint256[]`|The list of binStep|


### getOpenBinSteps

View function to return the list of open binSteps


```solidity
function getOpenBinSteps() external view override returns (uint256[] memory openBinStep);
```
**Returns**

|Name|Type|Description|
|----|----|-----------|
|`openBinStep`|`uint256[]`|The list of open binSteps|


### getAllLBPairs

View function to return all the LBPair of a pair of tokens


```solidity
function getAllLBPairs(IERC20 tokenX, IERC20 tokenY)
    external
    view
    override
    returns (LBPairInformation[] memory lbPairsAvailable);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`tokenX`|`IERC20`|The first token of the pair|
|`tokenY`|`IERC20`|The second token of the pair|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`lbPairsAvailable`|`LBPairInformation[]`|The list of available LBPairs|


### setLBPairImplementation

Set the LBPair implementation address

*Needs to be called by the owner*


```solidity
function setLBPairImplementation(address newLBPairImplementation) external override onlyOwner;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`newLBPairImplementation`|`address`|The address of the implementation|


### createLBPair

Create a liquidity bin LBPair for tokenX and tokenY


```solidity
function createLBPair(IERC20 tokenX, IERC20 tokenY, uint24 activeId, uint16 binStep)
    external
    override
    returns (ILBPair pair);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`tokenX`|`IERC20`|The address of the first token|
|`tokenY`|`IERC20`|The address of the second token|
|`activeId`|`uint24`|The active id of the pair|
|`binStep`|`uint16`|The bin step in basis point, used to calculate log(1 + binStep / 10_000)|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`pair`|`ILBPair`|The address of the newly created LBPair|


### setLBPairIgnored

Function to set whether the pair is ignored or not for routing, it will make the pair unusable by the router

*Needs to be called by the owner
Reverts if:
- The pair doesn't exist
- The ignored state is already in the same state*


```solidity
function setLBPairIgnored(IERC20 tokenX, IERC20 tokenY, uint16 binStep, bool ignored) external override onlyOwner;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`tokenX`|`IERC20`|The address of the first token of the pair|
|`tokenY`|`IERC20`|The address of the second token of the pair|
|`binStep`|`uint16`|The bin step in basis point of the pair|
|`ignored`|`bool`|Whether to ignore (true) or not (false) the pair for routing|


### setPreset

Sets the preset parameters of a bin step

*Needs to be called by the owner
Reverts if:
- The binStep is lower than the minimum bin step*


```solidity
function setPreset(
    uint16 binStep,
    uint16 baseFactor,
    uint16 filterPeriod,
    uint16 decayPeriod,
    uint16 reductionFactor,
    uint24 variableFeeControl,
    uint16 protocolShare,
    uint24 maxVolatilityAccumulator,
    bool isOpen
) external override onlyOwner;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`binStep`|`uint16`|The bin step in basis point, used to calculate the price|
|`baseFactor`|`uint16`|The base factor, used to calculate the base fee, baseFee = baseFactor * binStep|
|`filterPeriod`|`uint16`|The period where the accumulator value is untouched, prevent spam|
|`decayPeriod`|`uint16`|The period where the accumulator value is decayed, by the reduction factor|
|`reductionFactor`|`uint16`|The reduction factor, used to calculate the reduction of the accumulator|
|`variableFeeControl`|`uint24`|The variable fee control, used to control the variable fee, can be 0 to disable it|
|`protocolShare`|`uint16`|The share of the fees received by the protocol|
|`maxVolatilityAccumulator`|`uint24`|The max value of the volatility accumulator|
|`isOpen`|`bool`||


### setPresetOpenState

Sets if the preset is open or not to be used by users

*Needs to be called by the owner
Reverts if:
- The binStep doesn't have a preset
- The preset is already in the same state*


```solidity
function setPresetOpenState(uint16 binStep, bool isOpen) external override onlyOwner;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`binStep`|`uint16`|The bin step in basis point, used to calculate the price|
|`isOpen`|`bool`|Whether the preset is open or not|


### removePreset

Remove the preset linked to a binStep

*Needs to be called by the owner
Reverts if:
- The binStep doesn't have a preset*


```solidity
function removePreset(uint16 binStep) external override onlyOwner;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`binStep`|`uint16`|The bin step to remove|


### setFeesParametersOnPair

Function to set the fee parameter of a LBPair

*Needs to be called by the owner
Reverts if:
- The pair doesn't exist*


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
) external override onlyOwner;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`tokenX`|`IERC20`|The address of the first token|
|`tokenY`|`IERC20`|The address of the second token|
|`binStep`|`uint16`|The bin step in basis point, used to calculate the price|
|`baseFactor`|`uint16`|The base factor, used to calculate the base fee, baseFee = baseFactor * binStep|
|`filterPeriod`|`uint16`|The period where the accumulator value is untouched, prevent spam|
|`decayPeriod`|`uint16`|The period where the accumulator value is decayed, by the reduction factor|
|`reductionFactor`|`uint16`|The reduction factor, used to calculate the reduction of the accumulator|
|`variableFeeControl`|`uint24`|The variable fee control, used to control the variable fee, can be 0 to disable it|
|`protocolShare`|`uint16`|The share of the fees received by the protocol|
|`maxVolatilityAccumulator`|`uint24`|The max value of volatility accumulator|


### setLBHooksParametersOnPair

Function to set the hooks parameters of a pair

*Needs to be called by an address with the LB_HOOKS_MANAGER_ROLE
Reverts if:
- The pair doesn't exist
- The hooks is `address(0)` or the hooks flags are all false*


```solidity
function setLBHooksParametersOnPair(
    IERC20 tokenX,
    IERC20 tokenY,
    uint16 binStep,
    bytes32 hooksParameters,
    bytes calldata onHooksSetData
) external override onlyRole(LB_HOOKS_MANAGER_ROLE);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`tokenX`|`IERC20`|The address of the first token|
|`tokenY`|`IERC20`|The address of the second token|
|`binStep`|`uint16`|The bin step in basis point, used to calculate the price|
|`hooksParameters`|`bytes32`|The hooks parameters|
|`onHooksSetData`|`bytes`|The data to pass to the onHooksSet function|


### removeLBHooksOnPair

Function to remove the hooks contract from the pair

*Needs to be called by an address with the LB_HOOKS_MANAGER_ROLE
Reverts if:
- The pair doesn't exist*


```solidity
function removeLBHooksOnPair(IERC20 tokenX, IERC20 tokenY, uint16 binStep)
    external
    override
    onlyRole(LB_HOOKS_MANAGER_ROLE);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`tokenX`|`IERC20`|The address of the first token|
|`tokenY`|`IERC20`|The address of the second token|
|`binStep`|`uint16`|The bin step in basis point, used to calculate the price|


### setFeeRecipient

Function to set the recipient of the fees. This address needs to be able to receive ERC20s

*Needs to be called by the owner
Reverts if:
- The feeRecipient is `address(0)`
- The feeRecipient is the same as the current one*


```solidity
function setFeeRecipient(address feeRecipient) external override onlyOwner;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`feeRecipient`|`address`|The address of the recipient|


### setFlashLoanFee

Function to set the flash loan fee

*Needs to be called by the owner
Reverts if:
- The flashLoanFee is the same as the current one
- The flashLoanFee is above the maximum flash loan fee*


```solidity
function setFlashLoanFee(uint256 flashLoanFee) external override onlyOwner;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`flashLoanFee`|`uint256`|The value of the fee for flash loan|


### addQuoteAsset

Function to add an asset to the whitelist of quote assets

*Needs to be called by the owner
Reverts if:
- The quoteAsset is already whitelisted*


```solidity
function addQuoteAsset(IERC20 quoteAsset) external override onlyOwner;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`quoteAsset`|`IERC20`|The quote asset (e.g: NATIVE, USDC...)|


### removeQuoteAsset

Function to remove an asset from the whitelist of quote assets

*Needs to be called by the owner
Reverts if:
- The quoteAsset was not whitelisted*


```solidity
function removeQuoteAsset(IERC20 quoteAsset) external override onlyOwner;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`quoteAsset`|`IERC20`|The quote asset (e.g: NATIVE, USDC...)|


### _isPresetOpen


```solidity
function _isPresetOpen(bytes32 preset) internal pure returns (bool);
```

### _setFeeRecipient

Internal function to set the recipient of the fee


```solidity
function _setFeeRecipient(address feeRecipient) internal;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`feeRecipient`|`address`|The address of the recipient|


### forceDecay

Function to force the decay of the volatility accumulator of a pair

*Needs to be called by the owner*


```solidity
function forceDecay(ILBPair pair) external override onlyOwner;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`pair`|`ILBPair`|The pair to force the decay|


### _getLBPairInformation

Returns the LBPairInformation if it exists,
if not, then the address 0 is returned. The order doesn't matter


```solidity
function _getLBPairInformation(IERC20 tokenA, IERC20 tokenB, uint256 binStep)
    private
    view
    returns (LBPairInformation memory);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`tokenA`|`IERC20`|The address of the first token of the pair|
|`tokenB`|`IERC20`|The address of the second token of the pair|
|`binStep`|`uint256`|The bin step of the LBPair|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`LBPairInformation`|The LBPairInformation|


### _sortTokens

Private view function to sort 2 tokens in ascending order


```solidity
function _sortTokens(IERC20 tokenA, IERC20 tokenB) private pure returns (IERC20, IERC20);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`tokenA`|`IERC20`|The first token|
|`tokenB`|`IERC20`|The second token|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`IERC20`|The sorted first token|
|`<none>`|`IERC20`|The sorted second token|


### _setLBHooksParametersOnPair

Internal function to set a hooks contract to the pair


```solidity
function _setLBHooksParametersOnPair(
    IERC20 tokenX,
    IERC20 tokenY,
    uint16 binStep,
    bytes32 hooksParameters,
    bytes memory onHooksSetData
) internal;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`tokenX`|`IERC20`|The address of the first token|
|`tokenY`|`IERC20`|The address of the second token|
|`binStep`|`uint16`|The bin step in basis point, used to calculate the price|
|`hooksParameters`|`bytes32`|The hooks parameters|
|`onHooksSetData`|`bytes`|The data to pass to the onHooksSet function|


### hasRole

Returns whether the caller has the role or not, only the owner has the DEFAULT_ADMIN_ROLE


```solidity
function hasRole(bytes32 role, address account) public view override returns (bool);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`role`|`bytes32`|The role to check|
|`account`|`address`|The address to check|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bool`|Whether the account has the role or not|


### _grantRole

Grants a role to an address, the DEFAULT_ADMIN_ROLE can not be granted


```solidity
function _grantRole(bytes32 role, address account) internal override returns (bool);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`role`|`bytes32`|The role to grant|
|`account`|`address`|The address to grant the role to|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bool`|Whether the role has been granted or not|


