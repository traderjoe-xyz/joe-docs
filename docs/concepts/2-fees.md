---
sidebar_position: 2
sidebar_label: Fees
---

# Fees

Fees will be collected by the protocol to compensate liquidity providers for the trading activity that occurs. The total swap fee $f_s$ will have two
components, a base fee $f_b$ and a variable fee $f_v$ that is a function of instantaneous price volatility. The fee rate will be applied to the swap amount in each liquidity bin and distributed proportionally to the liquidity providers in that bin following a distribution to the protocol. Fees will be held separate from liquidity and claimable by liquidity providers.

## Base Fee

The base fee is similar to the Joe V1 0.3% fee. The exact % is set by the protocol owner using the `base factor` parameter and also depends on the `bin step`: $f_b = B*s$


## Variable Fee

The variable fee on the other hand depends on the volatility of the market. It will be affected by the frequency of the swaps, but doing large swap accross many bins (on large price movements) will also increase it. The variable fee is calculated per bin (k) using $f_v(k) = A (v_k*s)$

The variable fee is calculated using a set of parameters:
- `variableFeeControl`: Also called $A$ in the whitepaper. Used to control the variable fee, can be 0 to disable them.
- `filterPeriod`: If two swaps happen within this period, the accumulator value $v_k$ will  not be touched, to prevent spam.
- `decayPeriod`: Period where the accumulator value $v_k$ is halved.
- `reductionFactor`: Controls how fast the variable fee will evolve over time.
- `maxVolatilityAccumulated`: The max value for $v_k$.

<!-- TODO: add a configuration example ? -->

## Protocol Fees

A share of all the fees generated can be taken by the protocol owner. Protocol Fees are defined by the `protocolShare` parameter.