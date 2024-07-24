---
sidebar_position: 0
sidebar_label: Concentrated Liquidity
---

# Concentrated Liquidity

## Introduction

Liquidity in classic AMM (Joe V1/Uniswap V2) is distributed uniformly in the entire price range from 0 to infinity.

We can improve capital efficiency, especially for certain pairs where you can expect trades to occur within a tight range. Take USDC/USDT for example, where most trading happens between $0.99 and $1.01. In this case, liquidity outside of this range is largely untouched and would be better off used elsewhere.

With the Liquidity Book (LB), liquidity providers can instead provide liquidity within a specified price range of their choice - this is called **concentrated liquidity**. Using the USDC/USDT pair as an example again, if an LP chooses to provide liquidity between $0.99 and $1.01 then the LP will earn trading fees so long price is within that range.

## Bin Pricing

Liquidity Book allows liquidity to be distributed across **discrete bins** with fixed width. Liquidity can be exchanged at fixed price within each bin. Each bin represents a single price point and the difference between two consecutive bins is the **bin step**.

Take for example USDC/USDT again. If the current price is \$1 and the bin step is 1 basis point (i.e. 0.0001 or 0.01%), then the next consecutive bins up are $1 * 1.0001 = \$1.0001$, $1.0001 * 1.0001 = \$1.00020001$, etc. Note that this is the geometric sequence $1.0001^n$.

Bin steps are configurable parameters set by the pool creator. There can be **multiple** markets of the same pair but varying only in their bin step. Liquidity pools in Liquidity Book are uniquely identified by its tuple $(X, Y, s)$ of pooled assets $X$, $Y$ and bin step $s$.

## Liquidity Book vs Uniswap V3

- Uniswap V3 concentrate liquidity within a fixed bound with continuous `X * Y = k` curve.
- Liquidity Book discretizes liquidity into fixed width bins, with fixed price `X + Y = k` within each bin.
- TLDR; Uni-V3 is constant product between ticks, LB is constant sum within bins.

