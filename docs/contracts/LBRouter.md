---
sidebar_position: 3
sidebar_label: LBRouter
---

## LBRouter

Main contract to interact with to swap and manage liquidity on Joe V2 exchange.

### constructor

```solidity
constructor(contract ILBFactory _factory, contract IJoeFactory _oldFactory, contract IWAVAX _wavax) public
```

Constructor

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _factory | contract ILBFactory | LBFactory address |
| _oldFactory | contract IJoeFactory | Address of old factory (Joe V1) |
| _wavax | contract IWAVAX | Address of WAVAX |

### receive

```solidity
receive() external payable
```

_Receive function that only accept AVAX from the WAVAX contract_

### getIdFromPrice

```solidity
function getIdFromPrice(contract ILBPair _LBPair, uint256 _price) external view override returns (uint24)
```

Returns the approximate id corresponding to the inputted price.
Warning, the returned id may be inaccurate close to the start price of a bin

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _LBPair | contract ILBPair | The address of the LBPair |
| _price | uint256 | The price of y per x (multiplied by 1e36) |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| [0] | uint24 | The id corresponding to this price |

### getPriceFromId

```solidity
function getPriceFromId(contract ILBPair _LBPair, uint24 _id) external view override returns (uint256)
```

Returns the price corresponding to the inputted id

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _LBPair | contract ILBPair | The address of the LBPair |
| _id | uint24 | The id |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| [0] | uint256 | The price corresponding to this id |

### getSwapIn

```solidity
function getSwapIn(contract ILBPair _LBPair, uint256 _amountOut, bool _swapForY) public view override returns (uint256 amountIn, uint256 feesIn)
```

Simulate a swap in

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _LBPair | contract ILBPair | The address of the LBPair |
| _amountOut | uint256 | The amount of token to receive |
| _swapForY | bool | Whether you swap X for Y (true), or Y for X (false) |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| amountIn | uint256 | The amount of token to send in order to receive _amountOut token |
| feesIn | uint256 | The amount of fees paid in token sent |

### getSwapOut

```solidity
function getSwapOut(contract ILBPair _LBPair, uint256 _amountIn, bool _swapForY) external view override returns (uint256 amountOut, uint256 feesIn)
```

Simulate a swap out

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _LBPair | contract ILBPair | The address of the LBPair |
| _amountIn | uint256 | The amount of token sent |
| _swapForY | bool | Whether you swap X for Y (true), or Y for X (false) |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| amountOut | uint256 | The amount of token received if _amountIn tokenX are sent |
| feesIn | uint256 | The amount of fees paid in token sent |

### createLBPair

```solidity
function createLBPair(contract IERC20 _tokenX, contract IERC20 _tokenY, uint24 _activeId, uint16 _binStep) external override returns (contract ILBPair pair)
```

Create a liquidity bin LBPair for _tokenX and _tokenY using the factory

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
| pair | contract ILBPair | The address of the newly created LBPair |

### addLiquidity

```solidity
function addLiquidity(struct ILBRouter.LiquidityParameters _liquidityParameters) external override returns (uint256[] depositIds, uint256[] liquidityMinted)
```

Add liquidity while performing safety checks

_This function is compliant with fee on transfer tokens_

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _liquidityParameters | struct ILBRouter.LiquidityParameters | The liquidity parameters |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| depositIds | uint256[] | Bin ids where the liquidity was actually deposited |
| liquidityMinted | uint256[] | Amounts of LBToken minted for each bin |

### addLiquidityAVAX

```solidity
function addLiquidityAVAX(struct ILBRouter.LiquidityParameters _liquidityParameters) external payable override returns (uint256[] depositIds, uint256[] liquidityMinted)
```

Add liquidity with AVAX while performing safety checks

_This function is compliant with fee on transfer tokens_

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _liquidityParameters | struct ILBRouter.LiquidityParameters | The liquidity parameters |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| depositIds | uint256[] | Bin ids where the liquidity was actually deposited |
| liquidityMinted | uint256[] | Amounts of LBToken minted for each bin |

### removeLiquidity

```solidity
function removeLiquidity(contract IERC20 _tokenX, contract IERC20 _tokenY, uint16 _binStep, uint256 _amountXMin, uint256 _amountYMin, uint256[] _ids, uint256[] _amounts, address _to, uint256 _deadline) external override ensure(_deadline) returns (uint256 amountX, uint256 amountY)
```

Remove liquidity while performing safety checks

_This function is compliant with fee on transfer tokens_

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _tokenX | contract IERC20 | The address of token X |
| _tokenY | contract IERC20 | The address of token Y |
| _binStep | uint16 | The bin step of the LBPair |
| _amountXMin | uint256 | The min amount to receive of token X |
| _amountYMin | uint256 | The min amount to receive of token Y |
| _ids | uint256[] | The list of ids to burn |
| _amounts | uint256[] | The list of amounts to burn of each id in `_ids` |
| _to | address | The address of the recipient |
| _deadline | uint256 | The deadline of the tx |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| amountX | uint256 | Amount of token X returned |
| amountY | uint256 | Amount of token Y returned |

### removeLiquidityAVAX

```solidity
function removeLiquidityAVAX(contract IERC20 _token, uint16 _binStep, uint256 _amountTokenMin, uint256 _amountAVAXMin, uint256[] _ids, uint256[] _amounts, address payable _to, uint256 _deadline) external override ensure(_deadline) returns (uint256 amountToken, uint256 amountAVAX)
```

Remove AVAX liquidity while performing safety checks

_This function is **NOT** compliant with fee on transfer tokens.
This is wanted as it would make users pays the fee on transfer twice,
use the `removeLiquidity` function to remove liquidity with fee on transfer tokens._

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _token | contract IERC20 | The address of token |
| _binStep | uint16 | The bin step of the LBPair |
| _amountTokenMin | uint256 | The min amount to receive of token |
| _amountAVAXMin | uint256 | The min amount to receive of AVAX |
| _ids | uint256[] | The list of ids to burn |
| _amounts | uint256[] | The list of amounts to burn of each id in `_ids` |
| _to | address payable | The address of the recipient |
| _deadline | uint256 | The deadline of the tx |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| amountToken | uint256 | Amount of token returned |
| amountAVAX | uint256 | Amount of AVAX returned |

### swapExactTokensForTokens

```solidity
function swapExactTokensForTokens(uint256 _amountIn, uint256 _amountOutMin, uint256[] _pairBinSteps, contract IERC20[] _tokenPath, address _to, uint256 _deadline) external override ensure(_deadline) verifyInputs(_pairBinSteps, _tokenPath) returns (uint256 amountOut)
```

Swaps exact tokens for tokens while performing safety checks

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _amountIn | uint256 | The amount of token to send |
| _amountOutMin | uint256 | The min amount of token to receive |
| _pairBinSteps | uint256[] | The bin step of the pairs (0: V1, other values will use V2) |
| _tokenPath | contract IERC20[] | The swap path using the binSteps following `_pairBinSteps` |
| _to | address | The address of the recipient |
| _deadline | uint256 | The deadline of the tx |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| amountOut | uint256 | Output amount of the swap |

### swapExactTokensForAVAX

```solidity
function swapExactTokensForAVAX(uint256 _amountIn, uint256 _amountOutMinAVAX, uint256[] _pairBinSteps, contract IERC20[] _tokenPath, address payable _to, uint256 _deadline) external override ensure(_deadline) verifyInputs(_pairBinSteps, _tokenPath) returns (uint256 amountOut)
```

Swaps exact tokens for AVAX while performing safety checks

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _amountIn | uint256 | The amount of token to send |
| _amountOutMinAVAX | uint256 | The min amount of AVAX to receive |
| _pairBinSteps | uint256[] | The bin step of the pairs (0: V1, other values will use V2) |
| _tokenPath | contract IERC20[] | The swap path using the binSteps following `_pairBinSteps` |
| _to | address payable | The address of the recipient |
| _deadline | uint256 | The deadline of the tx |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| amountOut | uint256 | Output amount of the swap |

### swapExactAVAXForTokens

```solidity
function swapExactAVAXForTokens(uint256 _amountOutMin, uint256[] _pairBinSteps, contract IERC20[] _tokenPath, address _to, uint256 _deadline) external payable override ensure(_deadline) verifyInputs(_pairBinSteps, _tokenPath) returns (uint256 amountOut)
```

Swaps exact AVAX for tokens while performing safety checks

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _amountOutMin | uint256 | The min amount of token to receive |
| _pairBinSteps | uint256[] | The bin step of the pairs (0: V1, other values will use V2) |
| _tokenPath | contract IERC20[] | The swap path using the binSteps following `_pairBinSteps` |
| _to | address | The address of the recipient |
| _deadline | uint256 | The deadline of the tx |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| amountOut | uint256 | Output amount of the swap |

### swapTokensForExactTokens

```solidity
function swapTokensForExactTokens(uint256 _amountOut, uint256 _amountInMax, uint256[] _pairBinSteps, contract IERC20[] _tokenPath, address _to, uint256 _deadline) external override ensure(_deadline) verifyInputs(_pairBinSteps, _tokenPath) returns (uint256[] amountsIn)
```

Swaps tokens for exact tokens while performing safety checks

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _amountOut | uint256 | The amount of token to receive |
| _amountInMax | uint256 | The max amount of token to send |
| _pairBinSteps | uint256[] | The bin step of the pairs (0: V1, other values will use V2) |
| _tokenPath | contract IERC20[] | The swap path using the binSteps following `_pairBinSteps` |
| _to | address | The address of the recipient |
| _deadline | uint256 | The deadline of the tx |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| amountsIn | uint256[] | Input amounts for every step of the swap |

### swapTokensForExactAVAX

```solidity
function swapTokensForExactAVAX(uint256 _amountAVAXOut, uint256 _amountInMax, uint256[] _pairBinSteps, contract IERC20[] _tokenPath, address payable _to, uint256 _deadline) external override ensure(_deadline) verifyInputs(_pairBinSteps, _tokenPath) returns (uint256[] amountsIn)
```

Swaps tokens for exact AVAX while performing safety checks

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _amountAVAXOut | uint256 | The amount of AVAX to receive |
| _amountInMax | uint256 | The max amount of token to send |
| _pairBinSteps | uint256[] | The bin step of the pairs (0: V1, other values will use V2) |
| _tokenPath | contract IERC20[] | The swap path using the binSteps following `_pairBinSteps` |
| _to | address payable | The address of the recipient |
| _deadline | uint256 | The deadline of the tx |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| amountsIn | uint256[] | Input amounts for every step of the swap |

### swapAVAXForExactTokens

```solidity
function swapAVAXForExactTokens(uint256 _amountOut, uint256[] _pairBinSteps, contract IERC20[] _tokenPath, address _to, uint256 _deadline) external payable override ensure(_deadline) verifyInputs(_pairBinSteps, _tokenPath) returns (uint256[] amountsIn)
```

Swaps AVAX for exact tokens while performing safety checks

_will refund any excess sent_

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _amountOut | uint256 | The amount of tokens to receive |
| _pairBinSteps | uint256[] | The bin step of the pairs (0: V1, other values will use V2) |
| _tokenPath | contract IERC20[] | The swap path using the binSteps following `_pairBinSteps` |
| _to | address | The address of the recipient |
| _deadline | uint256 | The deadline of the tx |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| amountsIn | uint256[] | Input amounts for every step of the swap |

### swapExactTokensForTokensSupportingFeeOnTransferTokens

```solidity
function swapExactTokensForTokensSupportingFeeOnTransferTokens(uint256 _amountIn, uint256 _amountOutMin, uint256[] _pairBinSteps, contract IERC20[] _tokenPath, address _to, uint256 _deadline) external override ensure(_deadline) verifyInputs(_pairBinSteps, _tokenPath) returns (uint256 amountOut)
```

Swaps exact tokens for tokens while performing safety checks supporting for fee on transfer tokens

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _amountIn | uint256 | The amount of token to send |
| _amountOutMin | uint256 | The min amount of token to receive |
| _pairBinSteps | uint256[] | The bin step of the pairs (0: V1, other values will use V2) |
| _tokenPath | contract IERC20[] | The swap path using the binSteps following `_pairBinSteps` |
| _to | address | The address of the recipient |
| _deadline | uint256 | The deadline of the tx |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| amountOut | uint256 | Output amount of the swap |

### swapExactTokensForAVAXSupportingFeeOnTransferTokens

```solidity
function swapExactTokensForAVAXSupportingFeeOnTransferTokens(uint256 _amountIn, uint256 _amountOutMinAVAX, uint256[] _pairBinSteps, contract IERC20[] _tokenPath, address payable _to, uint256 _deadline) external override ensure(_deadline) verifyInputs(_pairBinSteps, _tokenPath) returns (uint256 amountOut)
```

Swaps exact tokens for AVAX while performing safety checks supporting for fee on transfer tokens

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _amountIn | uint256 | The amount of token to send |
| _amountOutMinAVAX | uint256 | The min amount of AVAX to receive |
| _pairBinSteps | uint256[] | The bin step of the pairs (0: V1, other values will use V2) |
| _tokenPath | contract IERC20[] | The swap path using the binSteps following `_pairBinSteps` |
| _to | address payable | The address of the recipient |
| _deadline | uint256 | The deadline of the tx |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| amountOut | uint256 | Output amount of the swap |

### swapExactAVAXForTokensSupportingFeeOnTransferTokens

```solidity
function swapExactAVAXForTokensSupportingFeeOnTransferTokens(uint256 _amountOutMin, uint256[] _pairBinSteps, contract IERC20[] _tokenPath, address _to, uint256 _deadline) external payable override ensure(_deadline) verifyInputs(_pairBinSteps, _tokenPath) returns (uint256 amountOut)
```

Swaps exact AVAX for tokens while performing safety checks supporting for fee on transfer tokens

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _amountOutMin | uint256 | The min amount of token to receive |
| _pairBinSteps | uint256[] | The bin step of the pairs (0: V1, other values will use V2) |
| _tokenPath | contract IERC20[] | The swap path using the binSteps following `_pairBinSteps` |
| _to | address | The address of the recipient |
| _deadline | uint256 | The deadline of the tx |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| amountOut | uint256 | Output amount of the swap |

### sweep

```solidity
function sweep(contract IERC20 _token, address _to, uint256 _amount) external override onlyFactoryOwner
```

Unstuck tokens that are sent to this contract by mistake

_Only callable by the factory owner_

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _token | contract IERC20 | The address of the token |
| _to | address | The address of the user to send back the tokens |
| _amount | uint256 | The amount to send |

### sweepLBToken

```solidity
function sweepLBToken(contract ILBToken _lbToken, address _to, uint256[] _ids, uint256[] _amounts) external override onlyFactoryOwner
```

Unstuck LBTokens that are sent to this contract by mistake

_Only callable by the factory owner_

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _lbToken | contract ILBToken | The address of the LBToken |
| _to | address | The address of the user to send back the tokens |
| _ids | uint256[] | The list of token ids |
| _amounts | uint256[] | The list of amounts to send |
