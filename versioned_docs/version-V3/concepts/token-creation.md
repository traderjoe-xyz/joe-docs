---
sidebar_position: 0
sidebar_label: Token Creation
---

# Token Creation

## Introduction

The magic begins at the token factory, where the token and bonding curve is created.

The steps to launch a token on Token Mill are:
1. Create token
2. Create bonding curve
3. Transfer ownership of token
4. Send tokens to bonding curve
5. Purchase initial tokens for creator and send to token locker
6. Enable trading

<p align="center">
  <img src="/img/factory.png" alt="Graph showing the different components of token creation" width="800px" />
</p>

## Token Template

Tokens are created from permissioned token templates to ensure every token launched through Token Mill is secure and free from malicious mechanisms. 

The standard template is a basic ERC-20 with the following properties:
- Immutable max supply
- No mint function / fully minted at creation
- 18 decimals
- Basic user inputs:
  1. Token owner address
  2. Token symbol and name
  3. Token supply

Over time more templates may be added.

## Token Locker

The token locker is a contract that facilitates token distribution, locking and vesting. Anyone can send their tokens to the locker and specify a beneficiary and vesting schedule -- typically the creator.

Token Mill offer creators the option of purchasing a portion of initial supply and sending it to the token locker.

## Creator Allocation

The bonding curve ensures that every token can be sold back into it, maintaining consistent liquidity. However, it also requires that all tokens, including those for creators, must be purchased from the curve.

To minimize this cost, creators can set up a curve where the initial tokens are inexpensive. Token Mill provides the option for creators to batch token creation with their first purchase, allowing them to secure the initial supply and avoid being frontrun by bots.
