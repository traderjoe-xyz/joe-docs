---
sidebar_position: 0
sidebar_label: Introduction
---

# Introduction

Trader Joe V1 was a fork of Uniswap V2, a constant product Automated Market Maker (AMM).

Trader Joe V2, officially called the Liquidity Book, is a novel AMM that aims to solve the shortcomings of Uniswap V3.

Like Uniswap V3, it is also a concentrated liquidity AMM with some subtle differences:

- Price ranges are discretized into bins instead of ticks
- Bin steps (or tick sizes) can be more than 1 basis point
- Bins use constant sum invariant instead of constant product
- Liquidity is aggregated vertically instead of horizontally
- Liquidity positions are fungible
- Liquidity positions are not restricted to uniform distribution across its price range; they can be distributed in any shape desired

