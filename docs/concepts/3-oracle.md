---
sidebar_position: 3
sidebar_label: Oracle
---

# Oracle

## Introduction

`LBPairs` are providing historical data not only for prices but also for **volatility accumulated** and **bin crossed**. The price data is characterized by the **active bin ID** of the pair. These values are aggregated over time and averages on specific periods can be fetched.

## Samples and Time Weighted Average

Swaps historical data must be saved in the storage of the contract. To reduce gas costs, these values are aggregated into **samples** that allow calculating **time weighted average** of the data stored (active ID of the pair, volatility accumulated and bin crossed). The frequency of the sample creation is determined by the `oracleSampleLifetime`. This will be the time precision of the oracle.

For every swap, the three values mentionned above will be added to the corresponding cumulative value of the sample, weighted by the time since the last value was added. For example, if the active ID of the pair doesn't change for 5 minutes, it will have more impact on the average active ID than if it only stays to this ID for a few seconds.

Sample values can be read by calling `getOracleSampleFrom`. This will return the three cumulative values at the time specified by the `timeDelta` input: `cumulativeId`,  `cumulativeVolatilityAccumulated` and `cumulativeBinCrossed`.

To calculate the average value of any of those three variables, `getOracleSampleFrom` needs to called on two different timestamps, and the average value will be:
$$ 
\textbf{Time Weighted Average}  = \frac{getOracleSampleFrom(t_2).value - getOracleSampleFrom(t_1).value}{timestamp(t_2) - timestamp(t_1)}
$$

## Oracle

The data **samples** are stored in an array that we consider as the **oracle**. To save gas again, samples are not added at the end of the array endlessly but are replaced in a rolling basis in what can be called a **circular buffer**. This means that the oldest sample will be replaced when a new one is created.

<p align="center">
  <img src="/img/sample_array.png" alt="Chart showing a sample being replaced" width="500px" />
  <figcaption>The sample 7 is replaced by the last sample created</figcaption>
</p>

The `oracleSampleLifetime` controls the frequency of samples creation. Every swap happening after more than the specified interval will create a new **sample**. By default, the oracle array only contains 2 samples, but it can be extended by anyone by calling `increaseOracleLength`.

