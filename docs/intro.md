---
sidebar_position: 0
sidebar_label: Introduction
slug: /
---


# Introduction

:::info
User Manual has been moved to https://help.traderjoexyz.com
:::

Joe V2 is a decentralized exchange based on Liquidity Book, a novel AMM protocol. 

It has the following improvements from the Joe V1 Dex: 
- Zero 0% slippage for swaps between ticks
- Dynamic fees to improve liquidity provider profitability


### Liquidity Book vs Uniswap V3

Both Liquidity Book and Uniswap V3 are concentrated liquidity AMMs with some subtle differences:
- Price ranges are discretized into bins instead of ticks
- Bin steps (or tick sizes) can be more than 1 basis point
- Bins use constant sum invariant instead of constant product
- Liquidity is aggregated vertically instead of horizontally
- Liquidity positions are fungible
- Liquidity positions are not restricted to uniform distribution across its price range; they can be distributed in any shape desired
- Swap fees have fixed + variable pricing, which allows the AMM to charge more fees when market experiences high volatility. 
