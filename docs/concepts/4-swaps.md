---
sidebar_position: 4
sidebar_label: Swaps
---

# Swaps

## Introduction

Swaps on Liquidity Book pairs have the same interface as Joe V1 pairs. Swaps can ask for a specific input or output and also work with native AVAX.

## Individual swap

A swap in a liquidity book pair will cross one or many bins inside the pair. Starting from the active bin, it will consume the liquidity of the bin until reaching out the desired amount or emptying the bin. When a bin is empty, liquidity will be taken on the next closest bin, at the exchange rate defined by the bin. This bin then becomes the active bin of the pair.

<!-- TODO: Needs a section on surge pricing -->

## Liquidity Book Router

Like Joe V1, swaps on Liquidity Book can be executed through a router contract called `LBRouter`. This contract will abstract some of the complexity of the swap and allow chained swaps accross several pairs.

Unlike Joe V1, several `LBPairs` with the same tokens can be created, differentiated by the `binStep` parameter. When asking the router to do a swap, every swap step will be described using {token In, token Out, bin step}. The `LBRouter` contract is also compatible with Joe V1 pairs. To swap on a V1 pair, `binStep` must be put to zero.

