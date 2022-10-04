---
sidebar_position: 3
sidebar_label: Oracle
---

# Oracle

## Introduction

`LBPairs` are providing a TWAP oracle for price but also volatility. The function `getOracleSampleFrom` can be called to get the time-weighted average for active IDs (translate to a price), volatility accumulated and bin crossed.

## Time-Weighted Average

To retrieve the historical data, you must call `getOracleSampleFrom`. This function takes the period to consider as the input. It will return a time-weighted average of the value: the most recent values will have more weight than the older ones. This can be summarized by the formula below:

For a set of measurements $M = [M(t-1), M(t-5), M(t-12), M(t-24)]$, fetching the time-wheighted average of the last 30 seconds:
$$
\overline{M} = \frac {29 * M(t-1) + 25 * M(t-5) + 18 * M(t-12) + 6 * M(t-24)} {29 + 25 + 18 + 6}
$$

## Data storage

Data is stored in a circular manner, meaning that every new value will replace the oldest value stored in the oracle object. This way a swap will only update a storage slot and not create a new one, which would be much more expensive in gas.

By default, the oracle will only store the last two swaps, but the length of the oracle array can be increased by calling `increaseOracleLength`.

## Security

Even if TWAP based oracles are meant to be more resilient to price manipulation, oracle feeds should always be used with extra caution.
