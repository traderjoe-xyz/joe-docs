---
sidebar_position: 2
sidebar_label: Fees
---

# Fees

## Introduction

In this section we discuss fees. There are two fees that the trader pays: the swap fee and the protocol fee.

The swap fee is paid to liquidity providers for the trading activity that occurs. The total swap fee ($f_s$) will have two components: a **base fee** ($f_b$) and a **variable fee** ($f_v$), which is a function of instantaneous price volatility. The fee rate will be applied to the swap amount in each liquidity bin and distributed proportionally to the liquidity providers in that bin following a distribution to the protocol. Fees will be held separate from liquidity and claimable by liquidity providers.

## Base Fee

The base fee is similar to the Joe V1 0.3% fee. The exact percentage is set by the protocol owner using the **base factor** ($B$) and the **bin step** ($s$):

$$
f_b = B \cdot s
$$

## Variable Fee

The variable fee on the other hand depends on the volatility of the market. It will be affected by the frequency of the swaps, but doing large swap accross many bins (on large price movements) will also increase it. The variable fee is calculated using the **variable fee parameter** ($A$), bin step ($s$) and the **volatility accumulator** ($v_k$):

$$
f_v(k) = A(v_k \cdot s) ^ 2
$$

## Volatility Accumulator

The **volatility accumulator** is the witness of the current volatility of the market. It will be calculated during a swap and will depend on two factors: the **volatility accumulated** from the previous swaps, and the **introduced volatility**.

**Volatility accumulated** is adjusted on every swap. The more swaps happening, the higher the volatility accumulated will be. The variable will follow the subsequent rules:

- If the previous swap happened since less than `filterPeriod`, it will be kept from the previous swap and the variable fee will stack up due to the **introduced volatility**.
- If the previous swap happened between the `filterPeriod` and the `decayPeriod`, the importance of the volatility accumulated during the previous swap will be lowered by the `reductionFactor`.
- If the `decayPeriod` is over, the volatility accumulated will be dropped and only the **introduced volatility** will matter.

This can be summarized by this formula from the whitepaper:

$$
  v_k = \begin{cases}
            v_{prior} + k, & t < t_l \\
            R * v_{prior} + k, & t_l < t < t_u \\
            k , & t_u < t
        \end{cases}
$$

Where $k$ is the **introduced volatility**, $t_l$ the `filterPeriod`, $t_u$ the `decayPeriod` and $R$ the `reductionFactor`. To avoid enormous fees, $v_k$ is capped by `maxVolatilityAccumulated`.

On the contract, $k$ is calculated as the difference between the active bin ID before and after the swap, as this directly show the amplitude of the swap.

## Protocol Fees

A share of all the fees is also taken by the protocol and distributed to JOE token holders via the StableJoeStaking contract. It is expressed as a variable, `protocolShare`, which is a percentage of the total swap fee. The maximum possible is 25%.
