---
sidebar_position: 0

sidebar_label: Concentrated Liquidity
---

# Concentrated Liquidity

## Introduction

In Trader Joe V1, which is a fork of Uniswap V2, liquidity was distributed uniformly in the entire price range from 0 to infinity.

This proved to be a colossal waste of liquidity, especially for certain pairs where you can expect trades to occur within a tight range. Take USDC/USDT for example, where most trading happens between $0.99 and $1.01. In this case, liquidity outside of this range is largely untouched and would be better off used elsewhere.

With the Liquidity Book (LB), liquidity providers can instead provide liquidity within a specified price range of their choice - this is called **concentrated liquidity**. Using the USDC/USDT pair as an example again, if an LP chooses to provide liquidity between $0.99 and $1.01 then the LP will earn trading fees so long price is within that range.

## Bins

To allow concentrated liquidity, the price curve is discretized into **bins**, which is similar to the tick concept in Uniswap V3. The main difference however, is that LB uses the **constant sum** price formula instead of the constant product formula.

What this means is that each bin represents a single price point and the price difference between two consecutive bins is the bin step.

Take for example USDC/USDT again. If the current price is \$1 and the bin step is 1 basis point (i.e. 0.0001 or 0.01%), then the next consecutive bins up are $1 * 1.0001 = \$1.0001$, $1.0001 * 1.0001 = \$1.00020001$, etc. Astute mathematicians will notice that this is the geometric sequence $1.0001^n$.

In addition to using a different pricing invariant, bin steps are **not** restricted to 1 basis point and is a parameter set by the pool creator. Because of this, there can be **multiple** markets of the same pair but varying only in their bin step. Put differently, if we say $X$ is asset X, $Y$ is asset Y and $s$ is the bin step, then each market is uniquely identified by its tuple $(X, Y, s)$.

## Bin Pricing & Math

As you dive into the contracts, you will find a lot of bin math that can be terribly confusing. This section aims to resolve any confusion.

Even though price of any given asset can range from 0 to infinity, we are constrained to 256 bits and the largest number a `uint256` can hold is $2^{256} - 1$.

However, we also need to account for very small fractions, so we use **128.128 binary fixed-point numbers** instead. These numbers use the left 128 bits for all numbers to the left of the decimal (i.e. the integers) and the right 128 bits for all numbers to the right of the decimal (i.e. the fractions). Thus the price range of every asset is now constrained to $[2^{-128}, 2^{128})$ instead; the maximum of which is already very, very large and the minimum of which is already very, very small. Not quite 0 and infinity, but pretty much close to it.

Now that we have the lower and upper bounds of price and we discretized the entire price curve into bins, **how many bins could we possibly have**?

Remember how the price of each bin was basically a geometric sequence $(1 + s)^i$ - we now need to find the maximum integer for $i$ such that the entire value is less than the upper limit of price, $2^{128}$.

In the whitepaper this is expressed as $argmax_i\left((1 + s)^i < 2^{128} \right)$.

Taking the smallest possible value of $s$ which is 1 basis point, we can solve this as follows:

$$
(1 + 0.0001)^i < 2^{128}
$$

$$
log_2(1.0001)^i < log_2(2^{128})
$$

$$
i \cdot log_2(1.0001) < 128
$$

$$
i < \frac{128}{log_2(1.0001)} \approx 887,273
$$

$$
i = 887,272
$$

The above equation shows how many bins are needed to cover the entire range when $i$ is a positive integer, so we account for when it is negative by doubling it which equals to $2 * 887,272 = 1,774,544$ bins.

However, remember that $i$ can also be negative, so the smallest signed integer that can fit this many bins is an `int24`. A quick sanity check shows that the largest integer for an `int24` is $2^{23} - 1 = 8,388,607$ which is still plenty large enough to hold the largest $i$, which is $887,273$.

So even though we previously said the upper and lower limits of price was $[2^{-128}, 2^{128})$, we can also define the limits using how many bins there could possibly be, which comes to $[(1 + s)^{2^{-23}}, (1+s)^{2^{23}})$. However, if we are to be extremely technical, **the actual limits will be the minimum of the two.**
