---
sidebar_position: 1
sidebar_label: Concentrated Liquidity
---

# Concentrated Liquidity

## Introduction

In Trader Joe V1, which is a fork of Uniswap V2, liquidity was distributed uniformly in the entire price range from 0 to infinity.

This proved to be a colossal waste of liquidity, especially for certain pairs where you can expect trades to occur within a tight range. Take USDC/USDT for example, where most trading happens between $0.99 and $1.01. In this case, liquidity outside of this range is largely untouched and would be better off used elsewhere.

With the Liquidity Book (LB), liquidity providers can instead provide liquidity within a specified price range of their choice - this is called **concentrated liquidity**. Using the USDC/USDT pair as an example again, if an LP chooses to provide liquidity between $0.99 and $1.01 then the LP will earn trading fees so long price is within that range.

## Bins

To allow concentrated liquidity, the price curve is discretized into **bins**, which is similar to the tick concept in Uniswap V3. The main difference however, is that LB uses the **constant sum** price formula instead of the constant product formula.

What this means is that each bin represents a single price point and the difference between two consecutive bins is the bin step.

Take for example USDC/USDT again. If the current price is \$1 and the bin step is 1 basis point (i.e. 0.0001 or 0.01%), then the next consecutive bins up are $1 * 1.0001 = \$1.0001$, $1.0001 * 1.0001 = \$1.00020001$, etc. Astute mathematicians will notice that this is the geometric sequence $1.0001^n$.

In addition to using a different pricing invariant, bin steps are **not** restricted to 1 basis point and is a parameter set by the pool creator. Because of this, there can be **multiple** markets of the same pair but varying only in their bin step. Put differently, given asset $X$, asset $Y$ and bin step $s$, each market is uniquely identified by its tuple $(X, Y, s)$.
