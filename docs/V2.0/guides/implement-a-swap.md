---
sidebar_position: 0
sidebar_label: Implement A Swap
---

# Implement A Swap

## Introduction

Like Joe V1, swaps on Joe V2 can be executed through a router contract called `LBRouter`. This contract will abstract some of the complexity of the swap, perform safety checks and will revert if certain conditions were to not be met. This is recommended way to use Joe V2 for most users.

The rest of the document describes:

- Which functions should be called to swap tokens
- How to use them in code examples

## Swap Functions

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

## Code Examples

#### 1. Swap 10 USDC for USDT using `swapExactTokensForTokens` with no intermediate swap paths:

```js
uint256 amountIn = 10e6;

USDC.approve(address(router), amountIn);

IERC20[] memory tokenPath = new IERC20[](2);
tokenPath[0] = USDC;
tokenPath[1] = USDT;
uint256[] memory pairBinSteps = new uint256[](1); // pairBinSteps[i] refers to the bin step for the market (x, y) where tokenPath[i] = x and tokenPath[i+1] = y
pairBinSteps[0] = 1;

(uint256 amountOut, ) = router.getSwapOut(pair, amountIn, true);
uint256 amountOutWithSlippage = amountOut * 99 / 100 // We allow for 1% slippage
uint256 amountOutReal = router.swapExactTokensForTokens(amountIn, amountOutWithSlippage, pairBinSteps, tokenPath, receiverAddress, block.timestamp);
```

#### 2. Swap 1 AVAX for USDT using `swapExactAVAXForTokens` with no intermediate swap paths:

```js
uint256 amountIn = 1e18;

IERC20[] memory tokenPath = new IERC20[](2);
tokenPath[0] = WAVAX;
tokenPath[1] = USDT;
uint256[] memory pairBinSteps = new uint256[](1);
pairBinSteps[0] = 25;

(uint256 amountOut, ) = router.getSwapOut(pairWavax, amountIn, false);
uint256 amountOutWithSlippage = amountOut * 99 / 100 // We allow for 1% slippage
router.swapExactAVAXForTokens{value: amountIn}(amountOutWithSlippage, pairBinSteps, tokenPath, receiverAddress, block.timestamp);
```

#### 3. Swap USDT to get 10 USDC output using `swapTokensForExactTokens` that routes through WAVAX. In this example, the first swap occurs through USDT/WAVAX V2 pool and the second swap occurs through WAVAX/USDC V1 pool:

```js
uint256 amountOut = 10e6;

USDT.approve(address(router), 11e6);

IERC20[] memory tokenPath;
uint256[] memory pairBinSteps;

tokenPath = new IERC20[](3);
tokenPath[0] = USDT;
tokenPath[1] = WAVAX;
tokenPath[2] = USDC;

pairBinSteps = new uint256[](2);
pairBinSteps[0] = 20;
pairBinSteps[1] = 0; // Bin step of 0 points to the Joe V1 pair

// We define amountInMax as an arbitrary amount of 11e6 here
uint256[] memory amountsIn = router.swapTokensForExactTokens(amountOut, 11e6, pairBinSteps, tokenPath, receiverAddress, block.timestamp);
```
