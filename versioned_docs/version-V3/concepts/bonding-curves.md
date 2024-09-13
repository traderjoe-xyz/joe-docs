---
sidebar_position: 1
sidebar_label: Bonding Curves
---

# Bonding Curves

## Introduction

A bonding curve is a mathematical model that defines the relationship between an asset's price and its circulating supply. Bonding curves are the foundation of all automated market makers (AMMs), ensuring that the asset's price always follows the curve. The xy=k curve in Uniswap V2 is a well-known example. Unlike Uniswap V2, however, Token Mill's bonding curves operate without the need for any external liquidity.

## Use Any Bonding Curve

A bonding curve is simply a pricing function $$P(x)$$ that defines how the token's price moves as the circulating supply increases.

Token Mill's key advantage is its flexibility, enabling the use of any pricing function, as long as each successive point on the curve is strictly increasing. 

The smart contract only requires an input array of $$n$$ price points along the curve, giving token creators full control over defining the curve themselves.

### Approximating The Curve

Token Mill has no knowledge of the pricing function formula used by the creator; instead, it accepts an array of price points along the graph and connects them with straight lines, creating an approximation of the desired function. 

Including more price points will improve the accuracy of the approximation but will also increase gas costs. In most cases, setting $$n=10$$ price points is sufficient to approximate the function with high accuracy.

<p align="center">
  <img src="/img/curve_approximation.png" alt="Graph comparing curve approximation using n=2 vs n=10" width="800px" />
</p>


## Understanding Bonding Curves

### Price vs Supply

Creators only need to provide two variables:

- Token max supply, $$x_{max}$$
- Array of price points of size $$n$$, $$[P_0, P_1, P_2, ..., P_n]$$, such that $$P_i < P_{i+1}$$

The chosen variables determines the price-supply relationship and how sensitive price is to token demand.

In the figure below, the pricing function is quadratic and price is increasing at an increasing rate from $$0$$ to $$x_{max}$$.

<p align="center">
  <img src="/img/price_supply.png" alt="Price supply graph of quadratic pricing function" width="400px" />
</p>

### Capacity - Market Maker Of Last Resort

The bonding curve is designed to absorb all tokens in circulation and act as the "market maker of last resort". The amount of captal ($$Y$$ tokens or quote tokens like USDC) that the pool can be absorb is the **capacity** and is defined as:

$$
C = y(x) = \int^x_0 P(x) dx
$$

Capacity can also be defined as the amount of $$Y$$ tokens a creator wishes to raise for issuing a total of $$x_{max}$$ amount of $$X$$ tokens. This is also equal to the **fully diluted value (FDV)** if all tokens were sold from the bonding curve.

Plot capacity or value sink, $$y(x)$$, against supply for the quadratic pricing function above will yield the graph below. From this graph we can deduce that 20% of capital will result in the bonding curve issuing 50% of tokens.

<p align="center">
  <img src="/img/capacity_supply.png" alt="Capacity supply graph of quadratic pricing function" width="400px" />
</p>

### General Form Function Templates

Coming up with your own pricing function is hard, so we have provided several [general form function templates](./pricing-function-templates) to help you.

## Bid & Ask Curves

Up to this point, we've only discussed a single bonding curve, but in reality, each token market operates with two distinct curves: a bid curve and an ask curve. Tokens are bought from the ask curve and sold to the bid curve.

The pricing formulas for the two curves can actually differ; the smart contract simply requires two arrays of size $$n$$ as input, where $$P_{bid}(x_i) \leq P_{ask}(x_i)$$.

A fee is levied solely on buys and is defined as the spread, $$P_{ask}(x_i)-P_{bid}(x_i)$$. When a token is bought from the curve, the fee is distributed and the remaining amount of $$Y$$ tokens are sent to the pool to ensure there is sufficient capital is available to absorb a token sale back to the curve.

One approach to constructing these curves is by using a general form function template to generate an array of ask prices and then scaling down each ask price by a factor $$(1-f)$$, where $$0<f<1$$, to create the corresponding array of bid prices. 

In this case, the fee $$f$$ is fixed and defines the spread between the two curves. However, the fee doesn’t have to be fixed. If desired, different fees can be applied at different price points, allowing the creator to customize the curves as needed.

More on [fees](./fees).

Below is a graph showing a quadratic pricing function with 1%$ fixed fee.

<p align="center">
  <img src="/img/bid_ask.png" alt="Bonding curve of quadratic pricing function with 1% spread" width="400px" />
</p>
