---
sidebar_position: 2
sidebar_label: Pricing Function Templates
---

# Pricing Function Templates

Token Mill offers several customizable pricing function templates to aid creators. The selection of a function depends on how you want the price to change as tokens are purchased from the bonding curve.

This section provides a basic overview of how these functions differ. For a more detailed mathematical explanation, please refer to the whitepaper.

A Desmos link is provided for each function template to help you visualize the curves.

> **Tip:** The area under the pricing/bonding curve is the FDV.

## Linear

Price increases as a steady rate.

([Desmos](https://www.desmos.com/calculator/vr2swfpyym))

<p align="center">
  <img src="/img/linear.png" alt="Linear pricing curve" width="400px" />
</p>

## Quadratic

Price increases slowly at first, but is increasing at an increasing rate.

Creators have to additional define capacity $$C$$.

([Desmos](https://www.desmos.com/calculator/cykq5aulcg))

<p align="center">
  <img src="/img/quadratic.png" alt="quadratic pricing curve" width="400px" />
</p>

## Exponential

A pronounced version of quadratic, in which the initial slope is flatter but the latter slope is steeper. Use this curve over quadratic if you want the initial purchases to be cheaper.

([Desmos](https://www.desmos.com/calculator/y2712ysgdo))

<p align="center">
  <img src="/img/exponential.png" alt="Exponential pricing curve" width="400px" />
</p>

## Logarithmic

The opposite of exponential - price is increasing at a decreasing rate. Use this if you want price and FDV to grow very fast initially ("up only").

([Desmos](https://www.desmos.com/calculator/6ti0sfqoyi))

<p align="center">
  <img src="/img/logarithmic.png" alt="Logarithmic pricing curve" width="400px" />
</p>

## Power

All the above functions can be made with the power function by adjusting the additional variable $$\alpha$$. 

To be honest, this is all you need! Hence why it's the default.

([Desmos](https://www.desmos.com/calculator/8bwx9qftd6))

<p align="center">
  <img src="/img/power.png" alt="Power pricing curve" width="800px" />
</p>

## Design Your Own!

Feel free to create your own design instead of using the templates provided—you're welcome to adjust the price points in the input array as needed.

Consider designing a curve that behaves differently after reaching a certain FDV (Fully Diluted Valuation). For instance, a sigmoid curve starts with a slow rise, accelerates in the middle, and then levels off as it approaches the end.
