---
sidebar_position: 0
sidebar_label: Implement A Swap
---

# Implement A Swap

## Introduction

Like Joe V1, swaps on Joe V2 can be executed through a router contract called `LBRouter`. This contract will abstract some of the complexity of the swap, perform safety checks and will revert if certain conditions were to not be met. This is recommended way to use Joe V2 for most users.

Next paragraphs will show how to understand and use swap functions, namely:
- Which functions should be called to swap tokens.
- How Joe V2 functions differentiate from Joe V1 functions.
- What are function arguments that are common for all functions and what are limitations to them.
- What function arguments that are specific to individual functions mean.
- How to use them in code examples.

## Swap functions

Swap functions can be broadly divided into two categories:

When the input amount is specified:
- `swapExactTokensForTokens`
- `swapExactTokensForAVAX`
- `swapExactAVAXForTokens`

When the desired output amount is specified:
- `swapTokensForExactTokens`
- `swapTokensForExactAVAX`
- `swapAVAXForExactTokens`

### When Input Amount Is Specified

- `swapExactTokensForTokens` - When you specify an exact amount of ERC-20 to swap for another ERC-20. E.g. USDC/USDT and you input USDC; router will then fetch how much USDT to expect as output and perform swap.
- `swapExactTokensForAVAX` - When you specify an exact amount of ERC-20 to swap for AVAX. E.g AVAX/USDC and you input USDC; router will then fetch how much AVAX to expect as output and perform swap.
- `swapExactAVAXForTokens` - When you specify an exact amount of AVAX to swap for an ERC-20. E.g AVAX/USDC and you input AVAX; router will then fetch how much USDC to expect as output and perform swap.

### When Output Amount Is Specified

- `swapTokensForExactTokens` - When you specify exact amount of ERC-20 that you want to receive. E.g. USDC/USDT and you input USDC; router will then fetch how much USDT to transfer from your wallet and perform swap.
- `swapTokensForExactAVAX` - When you specify exact amount of AVAX that you want to receive. E.g. AVAX/USDT and you input AVAX; router will then fetch how much USDT to transfer from your wallet and perform swap.
- `swapAVAXForExactTokens` - When you specify exact amount of ERC-20 that you want to receive. E.g. AVAX/USDT and you input USDT; router will then fetch how much AVAX to transfer from your wallet and perform swap.

Every function has specific arguments, that need to be given. There are two function signatures examples below. To get familiar with all possible options, visit Joe V2 repository - [interfaces/ILBRouter.sol](https://github.com/traderjoe-xyz/joe-V2/blob/main/src/interfaces/ILBRouter.sol) or [LBRouter.sol](https://github.com/traderjoe-xyz/joe-V2/blob/main/src/LBRouter.sol)

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

## Differences between Joe V1 and Joe V2

Swapping with Router provides experience similar to swapping on Joe V1 (Uniswap V2-style) from user perspective, with few differences:

1. There is necessity to provide additional `uint256[] memory _pairBinSteps` argument. `_pairBinSteps` needs to be used to determine exact `LBPair` unambiguously, as different markets exist (different bin steps for Joe V2 pairs as well as Joe V1 liquidity). 
2. Gas costs will vary not only depending on length of `tokenPath`, but also on amount of bins crossed during every swap.
3. Amount of events emitted may vary - there will be `swap` event emitted for every bin, that is used.
4. Fees are varying between markets and are dynamically adjusted based on volatility.

## Common Function Arguments

There are arguments, that need to be passed to every swap function, namely:
- `IERC20[] memory tokenPath` - Array, that consists of token addresses, that swap should go through.
- `uint256[] memory pairBinSteps` - Array, that consists of binSteps, which should be used. 
- `address to` - Address, that will receive tokens after swap.
- `uint256 deadline` - UNIX timestamp; transaction will revert if included in block, that has timestamp higher than `deadline` with error `LBRouter__DeadlineExceeded`.

While `to` and `deadline` arguments are straightforward, `tokenPath` and `pairBinSteps` and their limitations are explained below.

`LBPair` used for single swap is explicitly defined by: 
- 2 tokens from `tokenPath`.
- One value from `pairBinSteps`.

As multiple markets can exist for the same pair (different bin steps, plus Joe V1 liquidity), `pairVersion` argument needs to be included additionally to identify `LBPair` unambiguously.

Simplest `tokenPath` has 2 tokens: token that is transferred from user (token in), and token that is transferred to user (token out).
When such path is not possible (direct pair doesn't exist or doesn't yield best result), longer `tokenPath` can be specified. 

`tokenPath` argument:
1. Needs to be longer than `1`.
2. Needs to be longer by `1` than `pairBinSteps` array.
3. Needs to have `IERC20` type for every token (not `address` type).
4. User will pay swap fees on every pair used.
5. First `IERC20` in array is token in, last `IERC20` is token out.
6. When using functions that swap AVAX to another token, `tokenPath[0]` must be WAVAX.
7. When using functions that swap to AVAX from another token, `tokenPath[tokenPath.length]` must be WAVAX.

`pairBinSteps` argument:
1. Needs to be shorter by `1` than `tokenPath` array.
2. Needs to be longer than `0`.
3. For `pairBinSteps[i] = 0` Joe V1 pair is used.
4. Has to point to existing pairs, or will revert with error `LBRouter__PairNotCreated`.

## Function-Specific Arguments

### `swapExactTokensForAVAX` and `swapExactTokensForTokens`

`uint256 _amountIn` - Exact amount of token in that will be taken from user to swap for `_amountOutMinAVAX`/`_amountOutMin`.

`uint256 _amountOutMinAVAX`/`uint256 _amountOutMin` - _"slippage"_ - Minimum amount of token out, that will be received by `address to`. Will revert with `LBRouter__InsufficientAmountOut` error, if received less. 

### `swapTokensforExactAVAX` and `swapTokensforExactTokens`

`uint256 amountInMax` - _"slippage"_ - Maximum amount that can be taken from user to swap for `amountOut`. Will revert with `LBRouter__MaxAmountInExceeded` error, if more would need to be sent. 

`uint256 amountOut` - Exact amount of token out that will be received by `address to`.

### `swapExactAVAXForTokens` 

`uint256 _amountOutMin` - Minimum amount of token out, that will be received by `address to`. Will revert with `LBRouter__InsufficientAmountOut` error, if received less. 

AVAX amount is not specified, as it will be included in `value` field while sending transaction. 

### `swapAVAXForExactTokens`

`uint256 _amountOut` - Exact amount of token out that will be received by `address to` 

AVAX amount is not specified, as it will be included in `value` field while sending transaction. Any excess sent will be refunded. Will revert with `LBRouter__MaxAmountInExceeded` error, if not enough AVAX sent.

### `SupportingFeeOnTransferTokens`

Functions with `SupportingFeeOnTransferTokens` in name, namely: 
- `swapExactTokensForTokensSupportingFeeOnTransferTokens`
- `swapExactTokensForAVAXSupportingFeeOnTransferTokens`
- `swapExactAVAXForTokensSupportingFeeOnTransferTokens` 
should be used, when swapping tokens that send fee on every transfer, but only when using Joe V1 pools. Joe V2 pools can be used without `SupportingFeeOnTransferTokens` component.

## Code Examples

1. Simple swap with `swapExactTokensForTokens` function
```js
uint256 amountIn = 10e6;

USDC.approve(address(router), amountIn);

IERC20[] memory tokenList = new IERC20[](2);
tokenList[0] = USDC;
tokenList[1] = USDT;
uint256[] memory pairBinSteps = new uint256[](1);
pairBinSteps[0] = 1;

(uint256 amountOut, ) = router.getSwapOut(pair, amountIn, true);
uint256 amountOutReal = router.swapExactTokensForTokens(amountIn, amountOut - 1000, pairBinSteps, tokenList, DEV, block.timestamp);
```

2. Simple swap from AVAX using `swapExactAVAXForTokens` function

```js
uint256 amountIn = 1e18;

IERC20[] memory tokenList = new IERC20[](2);
tokenList[0] = WAVAX;
tokenList[1] = USDT;
uint256[] memory pairBinSteps = new uint256[](1);
pairBinSteps[0] = 25;

(uint256 amountOut, ) = router.getSwapOut(pairWavax, amountIn, false);

router.swapExactAVAXForTokens{value: amountIn}(amountOut - 1000, pairBinSteps, tokenList, DEV, block.timestamp);
```

3. Swap using Joe V1 pool with `swapTokensForExactTokens` function

```js
uint256 amountOut = 10e6;

USDT.approve(address(router), 11e6);

IERC20[] memory tokenList;
uint256[] memory pairBinSteps;

tokenList = new IERC20[](3);
tokenList[0] = USDT;
tokenList[1] = WAVAX;
tokenList[2] = USDC;

pairBinSteps = new uint256[](2);
pairBinSteps[0] = 20;
pairBinSteps[1] = 0; // points to Joe V1 pair

uint256[] memory amountsIn = router.swapTokensForExactTokens(amountOut, 11e6, pairBinSteps, tokenList, DEV, block.timestamp);
```