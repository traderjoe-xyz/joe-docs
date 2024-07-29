---
sidebar_position: 0
sidebar_label: Introduction
slug: /
---


# Introduction

:::info
V2.1 adds Gas Optimization, Factory Presets, and new Router and Quoter support. See [Key Changes](/versioned_docs/version-V2.1/key-changes.md) for details.
:::

Liquidity Book is a novel, highly-capital efficient Automated Market Maker (AMM) protocol. Its features include:
- **Zero Slippage:** Traders can swap tokens with zero slippage within bins. 
- **Surge Pricing:** Liquidity Providers earn additional dynamic fees during high market volatility. 
- **High Capital Efficiency:** Liquidity Book can support high volume trading with low liquidity requirements. 
- **Flexible Liquidity:** Liquidity Providers can build flexible liquidity distributions according to their strategy. 


### Liquidity Book vs Uniswap V3

Both Liquidity Book and Uniswap V3 are concentrated liquidity AMMs with some subtle differences:
- Price ranges are discretized into bins instead of ticks
- Bins use constant sum invariant instead of constant product
- Bin steps (or tick sizes) can be more than 1 basis point
- Liquidity is aggregated vertically instead of horizontally
- Liquidity positions are fungible
- Liquidity positions are not restricted to uniform distribution across its price range; they can be distributed in any shape desired
- Swap fees have fixed + variable pricing, which allows the AMM to charge more fees when the market experiences high volatility. 
