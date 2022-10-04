---
sidebar_position: 3
sidebar_label: Oracle
---

# Oracle

## Introduction

`LBPairs` are providing a TWAP oracle for price but also volatility. The function `getOracleSampleFrom` can be called to get cumulative value for active IDs (translate to a price), volatility accumulated and bin crossed.

## Time-Weighted Average

Return values of the `getOracleSampleFrom` are **cumulative**, meaning that they are the sum of all the values stored in the history of the pair. To get the average value on a defined period, two calls must be made:

$$ 
\textbf{T\!W\!A\!P}  = \frac{getOracleSampleFrom(t_2) - getOracleSampleFrom(t_1)}{timestamp(t_2) - timestamp(t_1)}
$$

A `oracleSampleLifetime` is defined, meaning that only one value per lifetime period will be stored, containing the sum of all the data generated during the period.

## Data storage

The oracle object is an array of **samples**. The `oracleSampleLifetime` defines the time between the creation of two samples: every swap within that period will update the current sample, and the first swap after the end of the sample's lifetime will create a brand new **sample**.

Data is stored in a circular manner, meaning that every new sample will replace the oldest one stored in the oracle array. This way, creating a new data point will only update a storage slot and not create a new one, which would be much more expensive in gas.

By default, the oracle will only store the last two samples, but the length of the oracle array can be increased by calling `increaseOracleLength`. Adding slots on the oracle array will allow calculating averages on longer periods.

## Security

Even if TWAP based oracles are meant to be more resilient to price manipulation, oracle feeds should always be used with extra caution.
