# LBRouter
[Git Source](https://github.com/traderjoe-xyz/joe-v2/blob/16f011d25e6bf6d0a0c479974345b623d491104f/src/LBRouter.sol)

**Inherits:**
[ILBRouter](./interfaces/ILBRouter.md)

**Author:**
Trader Joe

Main contract to interact with to swap and manage liquidity on Joe V2 exchange.


## State Variables
### _factory2_2

```solidity
ILBFactory private immutable _factory2_2;
```


### _factory2_1

```solidity
ILBFactory private immutable _factory2_1;
```


### _factoryV1

```solidity
IJoeFactory private immutable _factoryV1;
```


### _legacyFactory

```solidity
ILBLegacyFactory private immutable _legacyFactory;
```


### _legacyRouter

```solidity
ILBLegacyRouter private immutable _legacyRouter;
```


### _wnative

```solidity
IWNATIVE private immutable _wnative;
```


## Functions
### onlyFactoryOwner


```solidity
modifier onlyFactoryOwner();
```

### ensure


```solidity
modifier ensure(uint256 deadline);
```

### verifyPathValidity


```solidity
modifier verifyPathValidity(Path memory path);
```

### constructor

Constructor


```solidity
constructor(
    ILBFactory factory2_2,
    IJoeFactory factoryV1,
    ILBLegacyFactory legacyFactory,
    ILBLegacyRouter legacyRouter,
    ILBFactory factory2_1,
    IWNATIVE wnative
);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`factory2_2`|`ILBFactory`|Address of Joe V2.2 factory|
|`factoryV1`|`IJoeFactory`|Address of Joe V1 factory|
|`legacyFactory`|`ILBLegacyFactory`|Address of Joe V2 factory|
|`legacyRouter`|`ILBLegacyRouter`|Address of Joe V2 router|
|`factory2_1`|`ILBFactory`|Address of Joe V2.1 factory|
|`wnative`|`IWNATIVE`|Address of WNATIVE|


### receive

*Receive function that only accept NATIVE from the WNATIVE contract*


```solidity
receive() external payable;
```

### getFactory

View function to get the factory V2.1 address


```solidity
function getFactory() external view override returns (ILBFactory lbFactory);
```
**Returns**

|Name|Type|Description|
|----|----|-----------|
|`lbFactory`|`ILBFactory`|The address of the factory V2.1|


### getFactoryV2_1

View function to get the factory V2.1 address


```solidity
function getFactoryV2_1() external view override returns (ILBFactory lbFactory);
```
**Returns**

|Name|Type|Description|
|----|----|-----------|
|`lbFactory`|`ILBFactory`|The address of the factory V2.1|


### getLegacyFactory

View function to get the factory V2 address


```solidity
function getLegacyFactory() external view override returns (ILBLegacyFactory legacyLBfactory);
```
**Returns**

|Name|Type|Description|
|----|----|-----------|
|`legacyLBfactory`|`ILBLegacyFactory`|The address of the factory V2|


### getV1Factory

View function to get the factory V1 address


```solidity
function getV1Factory() external view override returns (IJoeFactory factoryV1);
```
**Returns**

|Name|Type|Description|
|----|----|-----------|
|`factoryV1`|`IJoeFactory`|The address of the factory V1|


### getLegacyRouter

View function to get the router V2 address


```solidity
function getLegacyRouter() external view override returns (ILBLegacyRouter legacyRouter);
```
**Returns**

|Name|Type|Description|
|----|----|-----------|
|`legacyRouter`|`ILBLegacyRouter`|The address of the router V2|


### getWNATIVE

View function to get the WNATIVE address


```solidity
function getWNATIVE() external view override returns (IWNATIVE wnative);
```
**Returns**

|Name|Type|Description|
|----|----|-----------|
|`wnative`|`IWNATIVE`|The address of WNATIVE|


### getIdFromPrice

Returns the approximate id corresponding to the inputted price.
Warning, the returned id may be inaccurate close to the start price of a bin


```solidity
function getIdFromPrice(ILBPair pair, uint256 price) external view override returns (uint24);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`pair`|`ILBPair`|The address of the LBPair|
|`price`|`uint256`|The price of y per x (multiplied by 1e36)|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint24`|The id corresponding to this price|


### getPriceFromId

Returns the price corresponding to the inputted id


```solidity
function getPriceFromId(ILBPair pair, uint24 id) external view override returns (uint256);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`pair`|`ILBPair`|The address of the LBPair|
|`id`|`uint24`|The id|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint256`|The price corresponding to this id|


### getSwapIn

Simulate a swap in


```solidity
function getSwapIn(ILBPair pair, uint128 amountOut, bool swapForY)
    public
    view
    override
    returns (uint128 amountIn, uint128 amountOutLeft, uint128 fee);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`pair`|`ILBPair`|The address of the LBPair|
|`amountOut`|`uint128`|The amount of token to receive|
|`swapForY`|`bool`|Whether you swap X for Y (true), or Y for X (false)|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`amountIn`|`uint128`|The amount of token to send in order to receive amountOut token|
|`amountOutLeft`|`uint128`|The amount of token Out that can't be returned due to a lack of liquidity|
|`fee`|`uint128`|The amount of fees paid in token sent|


### getSwapOut

Simulate a swap out


```solidity
function getSwapOut(ILBPair pair, uint128 amountIn, bool swapForY)
    external
    view
    override
    returns (uint128 amountInLeft, uint128 amountOut, uint128 fee);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`pair`|`ILBPair`|The address of the LBPair|
|`amountIn`|`uint128`|The amount of token sent|
|`swapForY`|`bool`|Whether you swap X for Y (true), or Y for X (false)|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`amountInLeft`|`uint128`|The amount of token In that can't be swapped due to a lack of liquidity|
|`amountOut`|`uint128`|The amount of token received if amountIn tokenX are sent|
|`fee`|`uint128`|The amount of fees paid in token sent|


### createLBPair

Create a liquidity bin LBPair for tokenX and tokenY using the factory


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
|`binStep`|`uint16`|The bin step in basis point, used to calculate log(1 + binStep)|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`pair`|`ILBPair`|The address of the newly created LBPair|


### addLiquidity

Add liquidity while performing safety checks

*This function is compliant with fee on transfer tokens*


```solidity
function addLiquidity(LiquidityParameters calldata liquidityParameters)
    external
    override
    returns (
        uint256 amountXAdded,
        uint256 amountYAdded,
        uint256 amountXLeft,
        uint256 amountYLeft,
        uint256[] memory depositIds,
        uint256[] memory liquidityMinted
    );
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`liquidityParameters`|`LiquidityParameters`|The liquidity parameters|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`amountXAdded`|`uint256`|The amount of token X added|
|`amountYAdded`|`uint256`|The amount of token Y added|
|`amountXLeft`|`uint256`|The amount of token X left (sent back to liquidityParameters.refundTo)|
|`amountYLeft`|`uint256`|The amount of token Y left (sent back to liquidityParameters.refundTo)|
|`depositIds`|`uint256[]`|The ids of the deposits|
|`liquidityMinted`|`uint256[]`|The amount of liquidity minted|


### addLiquidityNATIVE

Add liquidity with NATIVE while performing safety checks

*This function is compliant with fee on transfer tokens*


```solidity
function addLiquidityNATIVE(LiquidityParameters calldata liquidityParameters)
    external
    payable
    override
    returns (
        uint256 amountXAdded,
        uint256 amountYAdded,
        uint256 amountXLeft,
        uint256 amountYLeft,
        uint256[] memory depositIds,
        uint256[] memory liquidityMinted
    );
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`liquidityParameters`|`LiquidityParameters`|The liquidity parameters|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`amountXAdded`|`uint256`|The amount of token X added|
|`amountYAdded`|`uint256`|The amount of token Y added|
|`amountXLeft`|`uint256`|The amount of token X left (sent back to liquidityParameters.refundTo)|
|`amountYLeft`|`uint256`|The amount of token Y left (sent back to liquidityParameters.refundTo)|
|`depositIds`|`uint256[]`|The ids of the deposits|
|`liquidityMinted`|`uint256[]`|The amount of liquidity minted|


### removeLiquidity

Remove liquidity while performing safety checks

*This function is compliant with fee on transfer tokens*


```solidity
function removeLiquidity(
    IERC20 tokenX,
    IERC20 tokenY,
    uint16 binStep,
    uint256 amountXMin,
    uint256 amountYMin,
    uint256[] memory ids,
    uint256[] memory amounts,
    address to,
    uint256 deadline
) external override ensure(deadline) returns (uint256 amountX, uint256 amountY);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`tokenX`|`IERC20`|The address of token X|
|`tokenY`|`IERC20`|The address of token Y|
|`binStep`|`uint16`|The bin step of the LBPair|
|`amountXMin`|`uint256`|The min amount to receive of token X|
|`amountYMin`|`uint256`|The min amount to receive of token Y|
|`ids`|`uint256[]`|The list of ids to burn|
|`amounts`|`uint256[]`|The list of amounts to burn of each id in `_ids`|
|`to`|`address`|The address of the recipient|
|`deadline`|`uint256`|The deadline of the tx|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`amountX`|`uint256`|Amount of token X returned|
|`amountY`|`uint256`|Amount of token Y returned|


### removeLiquidityNATIVE

Remove NATIVE liquidity while performing safety checks

*This function is **NOT** compliant with fee on transfer tokens.
This is wanted as it would make users pays the fee on transfer twice,
use the `removeLiquidity` function to remove liquidity with fee on transfer tokens.*


```solidity
function removeLiquidityNATIVE(
    IERC20 token,
    uint16 binStep,
    uint256 amountTokenMin,
    uint256 amountNATIVEMin,
    uint256[] memory ids,
    uint256[] memory amounts,
    address payable to,
    uint256 deadline
) external override ensure(deadline) returns (uint256 amountToken, uint256 amountNATIVE);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`token`|`IERC20`|The address of token|
|`binStep`|`uint16`|The bin step of the LBPair|
|`amountTokenMin`|`uint256`|The min amount to receive of token|
|`amountNATIVEMin`|`uint256`|The min amount to receive of NATIVE|
|`ids`|`uint256[]`|The list of ids to burn|
|`amounts`|`uint256[]`|The list of amounts to burn of each id in `_ids`|
|`to`|`address payable`|The address of the recipient|
|`deadline`|`uint256`|The deadline of the tx|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`amountToken`|`uint256`|Amount of token returned|
|`amountNATIVE`|`uint256`|Amount of NATIVE returned|


### swapExactTokensForTokens

Swaps exact tokens for tokens while performing safety checks


```solidity
function swapExactTokensForTokens(
    uint256 amountIn,
    uint256 amountOutMin,
    Path memory path,
    address to,
    uint256 deadline
) external override ensure(deadline) verifyPathValidity(path) returns (uint256 amountOut);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`amountIn`|`uint256`|The amount of token to send|
|`amountOutMin`|`uint256`|The min amount of token to receive|
|`path`|`Path`|The path of the swap|
|`to`|`address`|The address of the recipient|
|`deadline`|`uint256`|The deadline of the tx|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`amountOut`|`uint256`|Output amount of the swap|


### swapExactTokensForNATIVE

Swaps exact tokens for NATIVE while performing safety checks


```solidity
function swapExactTokensForNATIVE(
    uint256 amountIn,
    uint256 amountOutMinNATIVE,
    Path memory path,
    address payable to,
    uint256 deadline
) external override ensure(deadline) verifyPathValidity(path) returns (uint256 amountOut);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`amountIn`|`uint256`|The amount of token to send|
|`amountOutMinNATIVE`|`uint256`|The min amount of NATIVE to receive|
|`path`|`Path`|The path of the swap|
|`to`|`address payable`|The address of the recipient|
|`deadline`|`uint256`|The deadline of the tx|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`amountOut`|`uint256`|Output amount of the swap|


### swapExactNATIVEForTokens

Swaps exact NATIVE for tokens while performing safety checks


```solidity
function swapExactNATIVEForTokens(uint256 amountOutMin, Path memory path, address to, uint256 deadline)
    external
    payable
    override
    ensure(deadline)
    verifyPathValidity(path)
    returns (uint256 amountOut);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`amountOutMin`|`uint256`|The min amount of token to receive|
|`path`|`Path`|The path of the swap|
|`to`|`address`|The address of the recipient|
|`deadline`|`uint256`|The deadline of the tx|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`amountOut`|`uint256`|Output amount of the swap|


### swapTokensForExactTokens

Swaps tokens for exact tokens while performing safety checks


```solidity
function swapTokensForExactTokens(
    uint256 amountOut,
    uint256 amountInMax,
    Path memory path,
    address to,
    uint256 deadline
) external override ensure(deadline) verifyPathValidity(path) returns (uint256[] memory amountsIn);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`amountOut`|`uint256`|The amount of token to receive|
|`amountInMax`|`uint256`|The max amount of token to send|
|`path`|`Path`|The path of the swap|
|`to`|`address`|The address of the recipient|
|`deadline`|`uint256`|The deadline of the tx|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`amountsIn`|`uint256[]`|Input amounts of the swap|


### swapTokensForExactNATIVE

Swaps tokens for exact NATIVE while performing safety checks


```solidity
function swapTokensForExactNATIVE(
    uint256 amountNATIVEOut,
    uint256 amountInMax,
    Path memory path,
    address payable to,
    uint256 deadline
) external override ensure(deadline) verifyPathValidity(path) returns (uint256[] memory amountsIn);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`amountNATIVEOut`|`uint256`|The amount of NATIVE to receive|
|`amountInMax`|`uint256`|The max amount of token to send|
|`path`|`Path`|The path of the swap|
|`to`|`address payable`|The address of the recipient|
|`deadline`|`uint256`|The deadline of the tx|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`amountsIn`|`uint256[]`|path amounts for every step of the swap|


### swapNATIVEForExactTokens

Swaps NATIVE for exact tokens while performing safety checks

*Will refund any NATIVE amount sent in excess to `msg.sender`*


```solidity
function swapNATIVEForExactTokens(uint256 amountOut, Path memory path, address to, uint256 deadline)
    external
    payable
    override
    ensure(deadline)
    verifyPathValidity(path)
    returns (uint256[] memory amountsIn);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`amountOut`|`uint256`|The amount of tokens to receive|
|`path`|`Path`|The path of the swap|
|`to`|`address`|The address of the recipient|
|`deadline`|`uint256`|The deadline of the tx|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`amountsIn`|`uint256[]`|path amounts for every step of the swap|


### swapExactTokensForTokensSupportingFeeOnTransferTokens

Swaps exact tokens for tokens while performing safety checks supporting for fee on transfer tokens


```solidity
function swapExactTokensForTokensSupportingFeeOnTransferTokens(
    uint256 amountIn,
    uint256 amountOutMin,
    Path memory path,
    address to,
    uint256 deadline
) external override ensure(deadline) verifyPathValidity(path) returns (uint256 amountOut);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`amountIn`|`uint256`|The amount of token to send|
|`amountOutMin`|`uint256`|The min amount of token to receive|
|`path`|`Path`|The path of the swap|
|`to`|`address`|The address of the recipient|
|`deadline`|`uint256`|The deadline of the tx|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`amountOut`|`uint256`|Output amount of the swap|


### swapExactTokensForNATIVESupportingFeeOnTransferTokens

Swaps exact tokens for NATIVE while performing safety checks supporting for fee on transfer tokens


```solidity
function swapExactTokensForNATIVESupportingFeeOnTransferTokens(
    uint256 amountIn,
    uint256 amountOutMinNATIVE,
    Path memory path,
    address payable to,
    uint256 deadline
) external override ensure(deadline) verifyPathValidity(path) returns (uint256 amountOut);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`amountIn`|`uint256`|The amount of token to send|
|`amountOutMinNATIVE`|`uint256`|The min amount of NATIVE to receive|
|`path`|`Path`|The path of the swap|
|`to`|`address payable`|The address of the recipient|
|`deadline`|`uint256`|The deadline of the tx|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`amountOut`|`uint256`|Output amount of the swap|


### swapExactNATIVEForTokensSupportingFeeOnTransferTokens

Swaps exact NATIVE for tokens while performing safety checks supporting for fee on transfer tokens


```solidity
function swapExactNATIVEForTokensSupportingFeeOnTransferTokens(
    uint256 amountOutMin,
    Path memory path,
    address to,
    uint256 deadline
) external payable override ensure(deadline) verifyPathValidity(path) returns (uint256 amountOut);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`amountOutMin`|`uint256`|The min amount of token to receive|
|`path`|`Path`|The path of the swap|
|`to`|`address`|The address of the recipient|
|`deadline`|`uint256`|The deadline of the tx|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`amountOut`|`uint256`|Output amount of the swap|


### sweep

Unstuck tokens that are sent to this contract by mistake

*Only callable by the factory owner*


```solidity
function sweep(IERC20 token, address to, uint256 amount) external override onlyFactoryOwner;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`token`|`IERC20`|The address of the token|
|`to`|`address`|The address of the user to send back the tokens|
|`amount`|`uint256`|The amount to send|


### sweepLBToken

Unstuck LBTokens that are sent to this contract by mistake

*Only callable by the factory owner*


```solidity
function sweepLBToken(ILBToken lbToken, address to, uint256[] calldata ids, uint256[] calldata amounts)
    external
    override
    onlyFactoryOwner;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`lbToken`|`ILBToken`|The address of the LBToken|
|`to`|`address`|The address of the user to send back the tokens|
|`ids`|`uint256[]`|The list of token ids|
|`amounts`|`uint256[]`|The list of amounts to send|


### _addLiquidity

Helper function to add liquidity


```solidity
function _addLiquidity(LiquidityParameters calldata liq, ILBPair pair)
    private
    ensure(liq.deadline)
    returns (
        uint256 amountXAdded,
        uint256 amountYAdded,
        uint256 amountXLeft,
        uint256 amountYLeft,
        uint256[] memory depositIds,
        uint256[] memory liquidityMinted
    );
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`liq`|`LiquidityParameters`|The liquidity parameter|
|`pair`|`ILBPair`|LBPair where liquidity is deposited|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`amountXAdded`|`uint256`|Amount of token X added|
|`amountYAdded`|`uint256`|Amount of token Y added|
|`amountXLeft`|`uint256`|Amount of token X left|
|`amountYLeft`|`uint256`|Amount of token Y left|
|`depositIds`|`uint256[]`|The list of deposit ids|
|`liquidityMinted`|`uint256[]`|The list of liquidity minted|


### _getAmountsIn

Helper function to return the amounts in


```solidity
function _getAmountsIn(Version[] memory versions, address[] memory pairs, IERC20[] memory tokenPath, uint256 amountOut)
    private
    view
    returns (uint256[] memory amountsIn);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`versions`|`Version[]`|The list of versions (V1, V2, V2_1 or V2_2)|
|`pairs`|`address[]`|The list of pairs|
|`tokenPath`|`IERC20[]`|The swap path|
|`amountOut`|`uint256`|The amount out|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`amountsIn`|`uint256[]`|The list of amounts in|


### _removeLiquidity

Helper function to remove liquidity


```solidity
function _removeLiquidity(
    ILBPair pair,
    uint256 amountXMin,
    uint256 amountYMin,
    uint256[] memory ids,
    uint256[] memory amounts,
    address to
) private returns (uint256 amountX, uint256 amountY);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`pair`|`ILBPair`|The address of the LBPair|
|`amountXMin`|`uint256`|The min amount to receive of token X|
|`amountYMin`|`uint256`|The min amount to receive of token Y|
|`ids`|`uint256[]`|The list of ids to burn|
|`amounts`|`uint256[]`|The list of amounts to burn of each id in `_ids`|
|`to`|`address`|The address of the recipient|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`amountX`|`uint256`|The amount of token X sent by the pair|
|`amountY`|`uint256`|The amount of token Y sent by the pair|


### _swapExactTokensForTokens

Helper function to swap exact tokens for tokens


```solidity
function _swapExactTokensForTokens(
    uint256 amountIn,
    address[] memory pairs,
    Version[] memory versions,
    IERC20[] memory tokenPath,
    address to
) private returns (uint256 amountOut);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`amountIn`|`uint256`|The amount of token sent|
|`pairs`|`address[]`|The list of pairs|
|`versions`|`Version[]`|The list of versions (V1, V2, V2_1 or V2_2)|
|`tokenPath`|`IERC20[]`|The swap path using the binSteps following `pairBinSteps`|
|`to`|`address`|The address of the recipient|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`amountOut`|`uint256`|The amount of token sent to `to`|


### _swapTokensForExactTokens

Helper function to swap tokens for exact tokens


```solidity
function _swapTokensForExactTokens(
    address[] memory pairs,
    Version[] memory versions,
    IERC20[] memory tokenPath,
    uint256[] memory amountsIn,
    address to
) private returns (uint256 amountOut);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`pairs`|`address[]`|The array of pairs|
|`versions`|`Version[]`|The list of versions (V1, V2, V2_1 or V2_2)|
|`tokenPath`|`IERC20[]`|The swap path using the binSteps following `pairBinSteps`|
|`amountsIn`|`uint256[]`|The list of amounts in|
|`to`|`address`|The address of the recipient|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`amountOut`|`uint256`|The amount of token sent to `to`|


### _swapSupportingFeeOnTransferTokens

Helper function to swap exact tokens supporting for fee on transfer tokens


```solidity
function _swapSupportingFeeOnTransferTokens(
    address[] memory pairs,
    Version[] memory versions,
    IERC20[] memory tokenPath,
    address to
) private;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`pairs`|`address[]`|The list of pairs|
|`versions`|`Version[]`|The list of versions (V1, V2, V2_1 or V2_2)|
|`tokenPath`|`IERC20[]`|The swap path using the binSteps following `pairBinSteps`|
|`to`|`address`|The address of the recipient|


### _getLBPairInformation

Helper function to return the address of the LBPair

*Revert if the pair is not created yet*


```solidity
function _getLBPairInformation(IERC20 tokenX, IERC20 tokenY, uint256 binStep, Version version)
    private
    view
    returns (address lbPair);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`tokenX`|`IERC20`|The address of the tokenX|
|`tokenY`|`IERC20`|The address of the tokenY|
|`binStep`|`uint256`|The bin step of the LBPair|
|`version`|`Version`|The version of the LBPair|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`lbPair`|`address`|The address of the LBPair|


### _getPair

Helper function to return the address of the pair (v1 or v2, according to `binStep`)

*Revert if the pair is not created yet*


```solidity
function _getPair(IERC20 tokenX, IERC20 tokenY, uint256 binStep, Version version) private view returns (address pair);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`tokenX`|`IERC20`|The address of the tokenX|
|`tokenY`|`IERC20`|The address of the tokenY|
|`binStep`|`uint256`|The bin step of the LBPair|
|`version`|`Version`|The version of the LBPair|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`pair`|`address`|The address of the pair of binStep `binStep`|


### _getPairs

Helper function to return a list of pairs


```solidity
function _getPairs(uint256[] memory pairBinSteps, Version[] memory versions, IERC20[] memory tokenPath)
    private
    view
    returns (address[] memory pairs);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`pairBinSteps`|`uint256[]`|The list of bin steps|
|`versions`|`Version[]`|The list of versions (V1, V2, V2_1 or V2_2)|
|`tokenPath`|`IERC20[]`|The swap path using the binSteps following `pairBinSteps`|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`pairs`|`address[]`|The list of pairs|


### _safeTransfer

Helper function to transfer tokens to `to`


```solidity
function _safeTransfer(IERC20 token, address to, uint256 amount) private;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`token`|`IERC20`|The address of the token|
|`to`|`address`|The address of the recipient|
|`amount`|`uint256`|The amount to send|


### _safeTransferFrom

Helper function to transfer tokens from `from` to `to`


```solidity
function _safeTransferFrom(IERC20 token, address from, address to, uint256 amount) private;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`token`|`IERC20`|The address of the token|
|`from`|`address`|The address of the sender|
|`to`|`address`|The address of the recipient|
|`amount`|`uint256`|The amount to send|


### _safeTransferNative

Helper function to transfer NATIVE to `to`


```solidity
function _safeTransferNative(address to, uint256 amount) private;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`to`|`address`|The address of the recipient|
|`amount`|`uint256`|The amount to send|


### _wNativeDepositAndTransfer

Helper function to deposit and transfer WNative to `to`


```solidity
function _wNativeDepositAndTransfer(address to, uint256 amount) private;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`to`|`address`|The address of the recipient|
|`amount`|`uint256`|The amount to deposit and transfer|


### _wNativeWithdrawAndTransfer

Helper function to withdraw and transfer WNative to `to`


```solidity
function _wNativeWithdrawAndTransfer(address to, uint256 amount) private;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`to`|`address`|The address of the recipient|
|`amount`|`uint256`|The amount to withdraw and transfer|


