---
sidebar_position: 3
sidebar_label: Swaps
---

# Swaps

## Introduction

Token swaps are conducted by calling the router by calling for a specific input or output of a pair of tokens, or with native currency `AVAX | BNB | ETH`.

## Individual Swap

Swaps in Liquidity Book may cross one or mre bins inside a token pair contract called `LBPair`. Starting from the active bin, it will consume the liquidity of the bin until reaching the desired amount or emptying the bin. When a bin is empty, liquidity will be taken in the next closest bin at the exchange rate defined by the bin. This bin then becomes the active bin of the pair.

<!-- TODO: Needs a section on surge pricing -->

## Liquidity Book Router

Swaps on Liquidity Book can be executed through a router contract called `LBRouter`. This contract will abstract some of the complexity of the swap and allow chained swaps accross several pairs.

On Liquidity Book, it is possible for several `LBPair` with the same tokens to be created, differentiated only by the `binStep` parameter.

When asking the router to do a swap, every swap step will be described using `(tokenIn, tokenOut, binStep)`.

The `LBRouter` contract is also compatible with Joe V1 pairs. To swap on a V1 pair, `binStep` must be set to zero.

<!-- TODO: Routing v2.0 across v2.1 pools -->
