---
sidebar_position: 4
sidebar_label: Orderbook
---

# Orderbook

On top of the supply curve lies an orderbook that facilitates p2p trading.

Trading is done through the orderbook first and then through the supply curve if there are no orders that can be filled.

This orderbook is similar to the Liquidity Book, where each bin defines a specific price point and orders are placed by depositing liquidity into that bin. 

At any point, there can only be one active price bin, and all bins to the left contain only the quote asset (e.g. USDC) and all bins to the right contain only the base asset (e.g. XYZ).

<p align="center">
  <img src="/img/active_bin.png" alt="Liquidity bin architecture" width="300px" />
</p>

However, there are a few differences:
- Bin deposits act as limit orders, i.e. the liquidity is removed when filled
- Limit orders can be partially filled
- Trading fees do not go to the depositor, they goto Trader Joe instead
- Only one subet of bins will be open for deposit and trading at any time
- Bins have a bin step size of 1bp only
- However, we can approximate larger bin steps using *bin spacing* (more on this below)

The last point is a unique feature that allows a market to offer the granularity different size bin steps as price evolves.

For example, when a token is in its infancy, it makes sense to have larger bin steps to facilitate price discovery. As the FDV of the token grows however, it would make more sense to have smaller bin steps to facilitate finer price granularity.

## Bin Spacing

The Token Mill orderbook introduces a new feature that is not present in Liquidity Book - **bin spacing**.

In the TM orderbook, all bins have 1bp bin steps centered at P=1. This is unlike LB, where bin steps can be larger than 1bp.

Price for a given bin ID, $i$, is $(1 + 0.0001)^i$, and since $i$ is an `int24` (and can thus, also be negative), this allows us to discretize the entire price range.


However, I mentioned above that the orderbook can approximate different size bin steps. This is done through bin spacing.

Instead of opening every bin for deposit and trading, only bins that are a multiple of the bin space are open. 

For example, if bin spacing is 5, then every 5th bin will be open for depositing and trading; the rest remain closed.

Using the formula above, this means the prices available for trading are: $1.0001^1$, $1.0001^5$, $1.0001^{10}$, etc.

Through bin spacing, we're therefore able to approximate different size bin steps:

$$
(1 + binStep)^i \approx 1.0001^{(binSpace + i)}
$$

## Different Size Bin Steps for Different Price Ranges

As token price, and thus FDV, grows, it makes sense that the market structure evolves as well. 

Creators can configure the bin step size for different price ranges.

In this example, the creator opts for larger bin steps as smaller valuations to facilitate price discovery, but as FDV grows, opts to reduce the bin step to facilitate finer price granularity.

<p align="center">
  <img src="/img/fdv.png" alt="Table showing different bin step as FDV evolves" width="800px" />
</p>
