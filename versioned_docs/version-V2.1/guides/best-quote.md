---
sidebar_position: 4
sidebar_label: Finding The Best Quote
---

# Finding The Best Quote

## Introduction

Finding the optimal quote for a givien tokens path can be obtained through the `LBQuoter` contract. This contract will find the best combinations of swaps accross the V1, V2 and V2.1 pairs in order to optimise cost.

The rest of the document describes:

- Which functions to call to get the optimal quote from an input and output amount.
- Code examples that illustrate use cases. 

## Find The Best Quote From Amount In

This function retrieves the best route of swaps for a given input amount.

```js
function findBestPathFromAmountIn(address[] calldata route, uint128 amountIn)
    public
    view
    returns (Quote memory quote)
```

The output of this function is quite substantial. Here are the specifications to understand it better:

```js
struct Quote {
    address[] route; // Path in the form of an array of token address to go through
    address[] pairs; // Address of the different pairs to do through
    uint256[] binSteps; // Bin step for each pair (0 for V1 pairs)
    ILBRouter.Version[] versions; // Versions to use for each pair
    uint128[] amounts; // The amounts for every step of the swap
    uint128[] virtualAmountsWithoutSlippage; // The virtual amounts of every step of the swap without slippage
    uint128[] fees; // The fees to pay for every step of the swap
}
```
### Code Example

In this example, we want to swap 10 USDC to USDT. A possible route is to go through the WAVAX route in between:

```js
address[] memory tokenPath = new address[](3);
tokenPath[0] = USDC;
tokenPath[1] = WAVAX;
tokenPath[2] = USDT;

uint128 amountIn = 10 * 10e6;

LBQuoter.Quote memory quote = quoter.findBestPathFromAmountIn(tokenPath, amountIn);
```

## Find The Best Quote From Amount Out

This function retrieves the best route of swaps for a given output amount.

```js
function findBestPathFromAmountOut(address[] calldata route, uint128 amountOut)
    public
    view
    returns (Quote memory quote)
```

### Code Example

In this example, we want to own 10 USDC and we would like to know how many USDT is required to perform the if we want to go through the WAVAX route:
```js
address[] memory tokenPath = new address[](3);
tokenPath[0] = USDT;
tokenPath[1] = WAVAX;
tokenPath[2] = USDC;

uint128 amountOut = 10 * 10e6;

LBQuoter.Quote memory quote = quoter.findBestPathFromAmountOut(tokenPath, amountOut);
```