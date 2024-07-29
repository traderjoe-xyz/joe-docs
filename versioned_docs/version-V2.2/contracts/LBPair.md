# LBPair
[Git Source](https://github.com/traderjoe-xyz/joe-v2/blob/16f011d25e6bf6d0a0c479974345b623d491104f/src/LBPair.sol)

**Inherits:**
[LBToken](/src/LBToken.sol/abstract.LBToken.md), [ReentrancyGuardUpgradeable](/src/libraries/ReentrancyGuardUpgradeable.sol/abstract.ReentrancyGuardUpgradeable.md), [Clone](/src/libraries/Clone.sol/abstract.Clone.md), [ILBPair](/src/interfaces/ILBPair.sol/interface.ILBPair.md)

**Author:**
Trader Joe

The Liquidity Book Pair contract is the core contract of the Liquidity Book protocol


## State Variables
### _MAX_TOTAL_FEE

```solidity
uint256 private constant _MAX_TOTAL_FEE = 0.1e18;
```


### implementation

```solidity
address public immutable override implementation;
```


### _factory

```solidity
ILBFactory private immutable _factory;
```


### _parameters

```solidity
bytes32 private _parameters;
```


### _reserves

```solidity
bytes32 private _reserves;
```


### _protocolFees

```solidity
bytes32 private _protocolFees;
```


### _bins

```solidity
mapping(uint256 => bytes32) private _bins;
```


### _tree

```solidity
TreeMath.TreeUint24 private _tree;
```


### _oracle

```solidity
OracleHelper.Oracle private _oracle;
```


### _hooksParameters

```solidity
bytes32 private _hooksParameters;
```


## Functions
### onlyFactory


```solidity
modifier onlyFactory();
```

### onlyProtocolFeeRecipient


```solidity
modifier onlyProtocolFeeRecipient();
```

### constructor

*Constructor for the Liquidity Book Pair contract that sets the Liquidity Book Factory*


```solidity
constructor(ILBFactory factory_);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`factory_`|`ILBFactory`|The Liquidity Book Factory|


### initialize

Initialize the Liquidity Book Pair fee parameters and active id

*Can only be called by the Liquidity Book Factory*


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
) external override onlyFactory initializer;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`baseFactor`|`uint16`|The base factor for the static fee|
|`filterPeriod`|`uint16`|The filter period for the static fee|
|`decayPeriod`|`uint16`|The decay period for the static fee|
|`reductionFactor`|`uint16`|The reduction factor for the static fee|
|`variableFeeControl`|`uint24`|The variable fee control for the static fee|
|`protocolShare`|`uint16`|The protocol share for the static fee|
|`maxVolatilityAccumulator`|`uint24`|The max volatility accumulator for the static fee|
|`activeId`|`uint24`|The active id of the Liquidity Book Pair|


### getFactory

Returns the Liquidity Book Factory


```solidity
function getFactory() external view override returns (ILBFactory factory);
```
**Returns**

|Name|Type|Description|
|----|----|-----------|
|`factory`|`ILBFactory`|The Liquidity Book Factory|


### getTokenX

Returns the token X of the Liquidity Book Pair


```solidity
function getTokenX() external pure override returns (IERC20 tokenX);
```
**Returns**

|Name|Type|Description|
|----|----|-----------|
|`tokenX`|`IERC20`|The address of the token X|


### getTokenY

Returns the token Y of the Liquidity Book Pair


```solidity
function getTokenY() external pure override returns (IERC20 tokenY);
```
**Returns**

|Name|Type|Description|
|----|----|-----------|
|`tokenY`|`IERC20`|The address of the token Y|


### getBinStep

Returns the bin step of the Liquidity Book Pair

*The bin step is the increase in price between two consecutive bins, in basis points.
For example, a bin step of 1 means that the price of the next bin is 0.01% higher than the price of the previous bin.*


```solidity
function getBinStep() external pure override returns (uint16);
```
**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint16`|binStep The bin step of the Liquidity Book Pair, in 10_000th|


### getReserves

Returns the reserves of the Liquidity Book Pair
This is the sum of the reserves of all bins, minus the protocol fees.


```solidity
function getReserves() external view override returns (uint128 reserveX, uint128 reserveY);
```
**Returns**

|Name|Type|Description|
|----|----|-----------|
|`reserveX`|`uint128`|The reserve of token X|
|`reserveY`|`uint128`|The reserve of token Y|


### getActiveId

Returns the active id of the Liquidity Book Pair

*The active id is the id of the bin that is currently being used for swaps.
The price of the active bin is the price of the Liquidity Book Pair and can be calculated as follows:
`price = (1 + binStep / 10_000) ^ (activeId - 2^23)`*


```solidity
function getActiveId() external view override returns (uint24 activeId);
```
**Returns**

|Name|Type|Description|
|----|----|-----------|
|`activeId`|`uint24`|The active id of the Liquidity Book Pair|


### getBin

Returns the reserves of a bin


```solidity
function getBin(uint24 id) external view override returns (uint128 binReserveX, uint128 binReserveY);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`id`|`uint24`|The id of the bin|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`binReserveX`|`uint128`|The reserve of token X in the bin|
|`binReserveY`|`uint128`|The reserve of token Y in the bin|


### getNextNonEmptyBin

Returns the next non-empty bin

*The next non-empty bin is the bin with a higher (if swapForY is true) or lower (if swapForY is false)
id that has a non-zero reserve of token X or Y.*


```solidity
function getNextNonEmptyBin(bool swapForY, uint24 id) external view override returns (uint24 nextId);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`swapForY`|`bool`|Whether the swap is for token Y (true) or token X (false|
|`id`|`uint24`|The id of the bin|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`nextId`|`uint24`|The id of the next non-empty bin|


### getProtocolFees

Returns the protocol fees of the Liquidity Book Pair


```solidity
function getProtocolFees() external view override returns (uint128 protocolFeeX, uint128 protocolFeeY);
```
**Returns**

|Name|Type|Description|
|----|----|-----------|
|`protocolFeeX`|`uint128`|The protocol fees of token X|
|`protocolFeeY`|`uint128`|The protocol fees of token Y|


### getStaticFeeParameters

Returns the static fee parameters of the Liquidity Book Pair


```solidity
function getStaticFeeParameters()
    external
    view
    override
    returns (
        uint16 baseFactor,
        uint16 filterPeriod,
        uint16 decayPeriod,
        uint16 reductionFactor,
        uint24 variableFeeControl,
        uint16 protocolShare,
        uint24 maxVolatilityAccumulator
    );
```
**Returns**

|Name|Type|Description|
|----|----|-----------|
|`baseFactor`|`uint16`|The base factor for the static fee|
|`filterPeriod`|`uint16`|The filter period for the static fee|
|`decayPeriod`|`uint16`|The decay period for the static fee|
|`reductionFactor`|`uint16`|The reduction factor for the static fee|
|`variableFeeControl`|`uint24`|The variable fee control for the static fee|
|`protocolShare`|`uint16`|The protocol share for the static fee|
|`maxVolatilityAccumulator`|`uint24`|The maximum volatility accumulator for the static fee|


### getLBHooksParameters

Gets the hooks parameters of the Liquidity Book Pair


```solidity
function getLBHooksParameters() external view override returns (bytes32);
```
**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bytes32`|The hooks parameters of the Liquidity Book Pair|


### getVariableFeeParameters

Returns the variable fee parameters of the Liquidity Book Pair


```solidity
function getVariableFeeParameters()
    external
    view
    override
    returns (uint24 volatilityAccumulator, uint24 volatilityReference, uint24 idReference, uint40 timeOfLastUpdate);
```
**Returns**

|Name|Type|Description|
|----|----|-----------|
|`volatilityAccumulator`|`uint24`|The volatility accumulator for the variable fee|
|`volatilityReference`|`uint24`|The volatility reference for the variable fee|
|`idReference`|`uint24`|The id reference for the variable fee|
|`timeOfLastUpdate`|`uint40`|The time of last update for the variable fee|


### getOracleParameters

Returns the oracle parameters of the Liquidity Book Pair


```solidity
function getOracleParameters()
    external
    view
    override
    returns (uint8 sampleLifetime, uint16 size, uint16 activeSize, uint40 lastUpdated, uint40 firstTimestamp);
```
**Returns**

|Name|Type|Description|
|----|----|-----------|
|`sampleLifetime`|`uint8`|The sample lifetime for the oracle|
|`size`|`uint16`|The size of the oracle|
|`activeSize`|`uint16`|The active size of the oracle|
|`lastUpdated`|`uint40`|The last updated timestamp of the oracle|
|`firstTimestamp`|`uint40`|The first timestamp of the oracle, i.e. the timestamp of the oldest sample|


### getOracleSampleAt

Returns the cumulative values of the Liquidity Book Pair at a given timestamp

*The cumulative values are the cumulative id, the cumulative volatility and the cumulative bin crossed.*


```solidity
function getOracleSampleAt(uint40 lookupTimestamp)
    external
    view
    override
    returns (uint64 cumulativeId, uint64 cumulativeVolatility, uint64 cumulativeBinCrossed);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`lookupTimestamp`|`uint40`|The timestamp at which to look up the cumulative values|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`cumulativeId`|`uint64`|The cumulative id of the Liquidity Book Pair at the given timestamp|
|`cumulativeVolatility`|`uint64`|The cumulative volatility of the Liquidity Book Pair at the given timestamp|
|`cumulativeBinCrossed`|`uint64`|The cumulative bin crossed of the Liquidity Book Pair at the given timestamp|


### getPriceFromId

Returns the price corresponding to the given id, as a 128.128-binary fixed-point number

*This is the trusted source of price information, always trust this rather than getIdFromPrice*


```solidity
function getPriceFromId(uint24 id) external pure override returns (uint256 price);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`id`|`uint24`|The id of the bin|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`price`|`uint256`|The price corresponding to this id|


### getIdFromPrice

Returns the id corresponding to the given price

*The id may be inaccurate due to rounding issues, always trust getPriceFromId rather than
getIdFromPrice*


```solidity
function getIdFromPrice(uint256 price) external pure override returns (uint24 id);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`price`|`uint256`|The price of y per x as a 128.128-binary fixed-point number|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`id`|`uint24`|The id of the bin corresponding to this price|


### getSwapIn

Simulates a swap in.

*If `amountOutLeft` is greater than zero, the swap in is not possible,
and the maximum amount that can be swapped from `amountIn` is `amountOut - amountOutLeft`.*


```solidity
function getSwapIn(uint128 amountOut, bool swapForY)
    external
    view
    override
    returns (uint128 amountIn, uint128 amountOutLeft, uint128 fee);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`amountOut`|`uint128`|The amount of token X or Y to swap in|
|`swapForY`|`bool`|Whether the swap is for token Y (true) or token X (false)|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`amountIn`|`uint128`|The amount of token X or Y that can be swapped in, including the fee|
|`amountOutLeft`|`uint128`|The amount of token Y or X that cannot be swapped out|
|`fee`|`uint128`|The fee of the swap|


### getSwapOut

Simulates a swap out.

*If `amountInLeft` is greater than zero, the swap out is not possible,
and the maximum amount that can be swapped is `amountIn - amountInLeft` for `amountOut`.*


```solidity
function getSwapOut(uint128 amountIn, bool swapForY)
    external
    view
    override
    returns (uint128 amountInLeft, uint128 amountOut, uint128 fee);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`amountIn`|`uint128`|The amount of token X or Y to swap in|
|`swapForY`|`bool`|Whether the swap is for token Y (true) or token X (false)|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`amountInLeft`|`uint128`|The amount of token X or Y that cannot be swapped in|
|`amountOut`|`uint128`|The amount of token Y or X that can be swapped out|
|`fee`|`uint128`|The fee of the swap|


### swap

Swap tokens iterating over the bins until the entire amount is swapped.
Token X will be swapped for token Y if `swapForY` is true, and token Y for token X if `swapForY` is false.
This function will not transfer the tokens from the caller, it is expected that the tokens have already been
transferred to this contract through another contract, most likely the router.
That is why this function shouldn't be called directly, but only through one of the swap functions of a router
that will also perform safety checks, such as minimum amounts and slippage.
The variable fee is updated throughout the swap, it increases with the number of bins crossed.
The oracle is updated at the end of the swap.


```solidity
function swap(bool swapForY, address to) external override returns (bytes32 amountsOut);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`swapForY`|`bool`|Whether you're swapping token X for token Y (true) or token Y for token X (false)|
|`to`|`address`|The address to send the tokens to|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`amountsOut`|`bytes32`|The encoded amounts of token X and token Y sent to `to`|


### flashLoan

Flash loan tokens from the pool to a receiver contract and execute a callback function.
The receiver contract is expected to return the tokens plus a fee to this contract.
The fee is calculated as a percentage of the amount borrowed, and is the same for both tokens.


```solidity
function flashLoan(ILBFlashLoanCallback receiver, bytes32 amounts, bytes calldata data) external override;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`receiver`|`ILBFlashLoanCallback`|The contract that will receive the tokens and execute the callback function|
|`amounts`|`bytes32`|The encoded amounts of token X and token Y to flash loan|
|`data`|`bytes`|Any data that will be passed to the callback function|


### mint

Mint liquidity tokens by depositing tokens into the pool.
It will mint Liquidity Book (LB) tokens for each bin where the user adds liquidity.
This function will not transfer the tokens from the caller, it is expected that the tokens have already been
transferred to this contract through another contract, most likely the router.
That is why this function shouldn't be called directly, but through one of the add liquidity functions of a
router that will also perform safety checks.

*Any excess amount of token will be sent to the `to` address.*


```solidity
function mint(address to, bytes32[] calldata liquidityConfigs, address refundTo)
    external
    override
    notAddressZeroOrThis(to)
    returns (bytes32 amountsReceived, bytes32 amountsLeft, uint256[] memory liquidityMinted);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`to`|`address`|The address that will receive the LB tokens|
|`liquidityConfigs`|`bytes32[]`|The encoded liquidity configurations, each one containing the id of the bin and the percentage of token X and token Y to add to the bin.|
|`refundTo`|`address`|The address that will receive the excess amount of tokens|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`amountsReceived`|`bytes32`|The amounts of token X and token Y received by the pool|
|`amountsLeft`|`bytes32`|The amounts of token X and token Y that were not added to the pool and were sent to `to`|
|`liquidityMinted`|`uint256[]`|The amounts of LB tokens minted for each bin|


### burn

Burn Liquidity Book (LB) tokens and withdraw tokens from the pool.
This function will burn the tokens directly from the caller


```solidity
function burn(address from, address to, uint256[] calldata ids, uint256[] calldata amountsToBurn)
    external
    override
    checkApproval(from, msg.sender)
    returns (bytes32[] memory amounts);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`from`|`address`|The address that will burn the LB tokens|
|`to`|`address`|The address that will receive the tokens|
|`ids`|`uint256[]`|The ids of the bins from which to withdraw|
|`amountsToBurn`|`uint256[]`|The amounts of LB tokens to burn for each bin|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`amounts`|`bytes32[]`|The amounts of token X and token Y received by the user|


### collectProtocolFees

Collect the protocol fees from the pool.


```solidity
function collectProtocolFees()
    external
    override
    nonReentrant
    onlyProtocolFeeRecipient
    returns (bytes32 collectedProtocolFees);
```
**Returns**

|Name|Type|Description|
|----|----|-----------|
|`collectedProtocolFees`|`bytes32`|The amount of protocol fees collected|


### increaseOracleLength

Increase the length of the oracle used by the pool


```solidity
function increaseOracleLength(uint16 newLength) external override nonReentrant;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`newLength`|`uint16`|The new length of the oracle|


### setStaticFeeParameters

Sets the static fee parameters of the pool

*Can only be called by the factory*


```solidity
function setStaticFeeParameters(
    uint16 baseFactor,
    uint16 filterPeriod,
    uint16 decayPeriod,
    uint16 reductionFactor,
    uint24 variableFeeControl,
    uint16 protocolShare,
    uint24 maxVolatilityAccumulator
) external override nonReentrant onlyFactory;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`baseFactor`|`uint16`|The base factor of the static fee|
|`filterPeriod`|`uint16`|The filter period of the static fee|
|`decayPeriod`|`uint16`|The decay period of the static fee|
|`reductionFactor`|`uint16`|The reduction factor of the static fee|
|`variableFeeControl`|`uint24`|The variable fee control of the static fee|
|`protocolShare`|`uint16`|The protocol share of the static fee|
|`maxVolatilityAccumulator`|`uint24`|The max volatility accumulator of the static fee|


### setHooksParameters

Sets the hooks parameter of the pool

*Can only be called by the factory*


```solidity
function setHooksParameters(bytes32 hooksParameters, bytes calldata onHooksSetData)
    external
    override
    nonReentrant
    onlyFactory;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`hooksParameters`|`bytes32`|The hooks parameter|
|`onHooksSetData`|`bytes`|The data to be passed to the onHooksSet function of the hooks contract|


### forceDecay

Forces the decay of the volatility reference variables

*Can only be called by the factory*


```solidity
function forceDecay() external override nonReentrant onlyFactory;
```

### batchTransferFrom

Overrides the batch transfer function to call the hooks before and after the transfer


```solidity
function batchTransferFrom(address from, address to, uint256[] calldata ids, uint256[] calldata amounts)
    public
    override(LBToken, ILBToken);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`from`|`address`|The address to transfer from|
|`to`|`address`|The address to transfer to|
|`ids`|`uint256[]`|The ids of the tokens to transfer|
|`amounts`|`uint256[]`|The amounts of the tokens to transfer|


### _tokenX

*Returns the address of the token X*


```solidity
function _tokenX() internal pure returns (IERC20);
```
**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`IERC20`|The address of the token X|


### _tokenY

*Returns the address of the token Y*


```solidity
function _tokenY() internal pure returns (IERC20);
```
**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`IERC20`|The address of the token Y|


### _binStep

*Returns the bin step of the pool, in basis points*


```solidity
function _binStep() internal pure returns (uint16);
```
**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint16`|The bin step of the pool|


### _getNextNonEmptyBin

*Returns next non-empty bin*


```solidity
function _getNextNonEmptyBin(bool swapForY, uint24 id) internal view returns (uint24);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`swapForY`|`bool`|Whether the swap is for Y|
|`id`|`uint24`|The id of the bin|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint24`|The id of the next non-empty bin|


### _onlyFactory

*Reverts if the caller is not the factory*


```solidity
function _onlyFactory() private view;
```

### _getFlashLoanFees

*Returns the encoded fees amounts for a flash loan*


```solidity
function _getFlashLoanFees(bytes32 amounts) private view returns (bytes32);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`amounts`|`bytes32`|The amounts of the flash loan|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bytes32`|The encoded fees amounts|


### _setStaticFeeParameters

*Sets the static fee parameters of the pair*


```solidity
function _setStaticFeeParameters(
    bytes32 parameters,
    uint16 baseFactor,
    uint16 filterPeriod,
    uint16 decayPeriod,
    uint16 reductionFactor,
    uint24 variableFeeControl,
    uint16 protocolShare,
    uint24 maxVolatilityAccumulator
) internal;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`parameters`|`bytes32`|The current parameters of the pair|
|`baseFactor`|`uint16`|The base factor of the static fee|
|`filterPeriod`|`uint16`|The filter period of the static fee|
|`decayPeriod`|`uint16`|The decay period of the static fee|
|`reductionFactor`|`uint16`|The reduction factor of the static fee|
|`variableFeeControl`|`uint24`|The variable fee control of the static fee|
|`protocolShare`|`uint16`|The protocol share of the static fee|
|`maxVolatilityAccumulator`|`uint24`|The max volatility accumulator of the static fee|


### _mintBins

*Helper function to mint liquidity in each bin in the liquidity configurations*


```solidity
function _mintBins(bytes32[] calldata liquidityConfigs, bytes32 amountsReceived, address to, MintArrays memory arrays)
    private
    returns (bytes32 amountsLeft);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`liquidityConfigs`|`bytes32[]`|The liquidity configurations|
|`amountsReceived`|`bytes32`|The amounts received|
|`to`|`address`|The address to mint the liquidity to|
|`arrays`|`MintArrays`|The arrays to store the results|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`amountsLeft`|`bytes32`|The amounts left|


### _updateBin

*Helper function to update a bin during minting*


```solidity
function _updateBin(uint16 binStep, uint24 activeId, uint24 id, bytes32 maxAmountsInToBin, bytes32 parameters)
    internal
    returns (uint256 shares, bytes32 amountsIn, bytes32 amountsInToBin);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`binStep`|`uint16`|The bin step of the pair|
|`activeId`|`uint24`|The id of the active bin|
|`id`|`uint24`|The id of the bin|
|`maxAmountsInToBin`|`bytes32`|The maximum amounts in to the bin|
|`parameters`|`bytes32`|The parameters of the pair|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`shares`|`uint256`|The amount of shares minted|
|`amountsIn`|`bytes32`|The amounts in|
|`amountsInToBin`|`bytes32`|The amounts in to the bin|


