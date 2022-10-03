---
sidebar_position: 0
sidebar_label: Implement A Swap
---

# Implement a Swap

## Introduction

Like Joe v1, swaps on Joe v2 can be executed through a router contract called `LBRouter`. This contract will abstract some of the complexity of the swap, perform safety checks and will revert if certain conditions were to not be met. This is recommended way to use Joe v2 for most users.

Swapping with Router provides experience similar to swapping on Joe v1 (Uniswap v2-style) from user perspective, with few differences:

1. There is necessity to provide additional `uint256[] memory _pairBinSteps` argument. `_pairBinSteps` needs to be used to determine exact `LBPair` unambiguously, as different markets exist (different bin steps for Joe v2 pairs as well as Joe v1 liquidity). 
2. Gas costs will vary not only depending on length of `tokenPath`, but also on amount of bins crossed during every swap.
3. Amount of events emitted may vary - there will be `swap` event emitted for every bin, that is used.
4. Fees are varying between markets and dynamically adjusted based on volatility.

There are 9 different functions, that are possible to use for swapping. This documentation will not go in details into every of them, as most use similar concepts.

```js
    // Swaps exact tokens for tokens while performing safety checks
    function swapExactTokensForTokens(
        uint256 amountIn,
        uint256 amountOutMin,
        uint256[] memory pairBinSteps,
        IERC20[] memory tokenPath,
        address to,
        uint256 deadline
    ) external returns (uint256 amountOut);

    // Swaps tokens for exact tokens while performing safety checks
    function swapTokensForExactTokens(
        uint256 amountOut,
        uint256 amountInMax,
        uint256[] memory pairBinSteps,
        IERC20[] memory tokenPath,
        address to,
        uint256 deadline
    ) external returns (uint256[] memory amountsIn);
```

To get familiar with all possible options, visit DEX v2 repository - [interfaces/ILBRouter.sol](https://github.com/traderjoe-xyz/joe-v2/blob/main/src/interfaces/ILBRouter.sol) or [LBRouter.sol](https://github.com/traderjoe-xyz/joe-v2/blob/main/src/LBRouter.sol)

## Common function arguments

`IERC20[] memory tokenPath` - array, that consists of token addresses, that swap should go through.
Simplest `tokenPath` has 2 tokens: token that is transferred from user (token in), and token that is transferred to user (token out).
When such path is not possible (direct pair doesn't exist or doesn't yield best result), longer `tokenPath` can be specified. 
Pair is explicitly defined by: 
- 2 tokens from `tokenPath`,
- one value from `pairBinSteps`.

As there can exist multiple markets for the same pair (different bin steps, plus DEX v1 liquidity), `pairVersion` argument needs to be included additionally to identify `LBPair` unambiguously.

`tokenPath` - array, that consists of tokens, that swap should go through:
1. Needs to be longer than `1`.
2. Needs to be longer by `1` than `pairBinSteps` array.
3. Needs to have `IERC20` type for every token (not `address` type).
4. User will pay swap fees on every pair used.
5. First `IERC20` in array is token in, last `IERC20` is token out.
6. When using functions that swap AVAX to another token, `tokenPath[0]` must be WAVAX.
7. When using functions that swap to AVAX from another token, `tokenPath[tokenPath.length]` must be WAVAX.

`uint256[] memory pairBinSteps` - array, that consists of binSteps, which should be used. 
1. Needs to be shorter by `1` than `tokenPath` array.
2. Needs to be longer than `0`.
3. For `pairBinSteps[i] = 0` DEX v1 pair is used.
4. Has to point to existing pairs, or will revert with error `LBRouter__PairNotCreated`.

`address to` - address, that will receive tokens after swap.

`uint256 deadline` - UNIX timestamp; transaction will revert if included in block, that has timestamp higher than `deadline` with error `LBRouter__DeadlineExceeded`.

## Function-specific arguments

#### swapExactTokensForAVAX and swapExactTokensForTokens

`uint256 _amountIn` - exact amount of token in that will be taken from user to swap for `_amountOutMinAVAX`/`_amountOutMin`.

`uint256 _amountOutMinAVAX`/`uint256 _amountOutMin` - _"slippage"_ - minimum amount of token out, that will be received by `address to`. Will revert with `LBRouter__InsufficientAmountOut` error, if received less. 

#### swapTokensforExactAVAX and swapTokensforExactTokens

`uint256 amountInMax` - _"slippage"_ - maximum amount that can be taken from user to swap for `amountOut`. Will revert with `LBRouter__MaxAmountInExceeded` error, if more would need to be sent. 

`uint256 amountOut` - exact amount of token out that will be received by `address to`.

#### swapExactAVAXForTokens 

`uint256 _amountOutMin` - minimum amount of token out, that will be received by `address to`. Will revert with `LBRouter__InsufficientAmountOut` error, if received less. 

AVAX amount is not specified, as it will be included in `value` field while sending transaction. 

#### swapAVAXForExactTokens

`uint256 _amountOut` - exact amount of token out that will be received by `address to` 

AVAX amount is not specified, as it will be included in `value` field while sending transaction. Any excess sent will be refunded. Will revert with `LBRouter__MaxAmountInExceeded` error, if not enough AVAX sent.

#### SupportingFeeOnTransferTokens

Functions with `SupportingFeeOnTransferTokens` in name, namely: `swapExactTokensForTokensSupportingFeeOnTransferTokens`, `swapExactTokensForAVAXSupportingFeeOnTransferTokens`, `swapExactAVAXForTokensSupportingFeeOnTransferTokens` should be used, when swapping tokens that send fee on every transfer, but only when using DEX v1 pools. DEX v2 pools can be used without `SupportingFeeOnTransferTokens` component.


## Code examples

1. Simple swap with `swapExactTokensForTokens` function
```js
uint256 amountIn = 1e18;

token6D.mint(DEV, amountIn);
token6D.approve(address(router), amountIn);

IERC20[] memory tokenList = new IERC20[](2);
tokenList[0] = token6D;
tokenList[1] = token18D;
uint256[] memory pairBinSteps = new uint256[](1);
pairBinSteps[0] = 25;

(uint256 amountOut, ) = router.getSwapOut(pair, amountIn, true);
uint256 amountOutReal = router.swapExactTokensForTokens(amountIn, amountOut - 1000, pairBinSteps, tokenList, DEV, block.timestamp);
```

2. Simple swap from AVAX using `swapExactAVAXForTokens` function
```js
uint256 amountIn = 1e18;

IERC20[] memory tokenList = new IERC20[](2);
tokenList[0] = wavax;
tokenList[1] = token6D;
uint256[] memory pairBinSteps = new uint256[](1);
pairBinSteps[0] = 10;

(uint256 amountOut, ) = router.getSwapOut(pairWavax, amountIn, false);

router.swapExactAVAXForTokens{value: amountIn}(amountOut - 1000, pairBinSteps, tokenList, DEV, block.timestamp);
```

3. Swap using DEX v1 pool with `swapTokensForExactTokens` function

```js
uint256 amountOut = 1e6;
token6D.mint(DEV, 100e18);
token6D.approve(address(router), 100e18);

IERC20[] memory tokenList;
uint256[] memory pairBinSteps;

tokenList = new IERC20[](3);
tokenList[0] = token6D;
tokenList[1] = token12D;
tokenList[2] = usdc;

pairBinSteps = new uint256[](2);
pairBinSteps[0] = 20;
pairBinSteps[1] = 0; // points to DEX v1 pair

uint256[] memory amountsIn = router.swapTokensForExactTokens(amountOut, 100e18, pairBinSteps, tokenList, DEV, block.timestamp);
```