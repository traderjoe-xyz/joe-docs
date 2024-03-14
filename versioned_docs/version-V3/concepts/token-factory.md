---
sidebar_position: 0
sidebar_label: Token Factory
---

# Token Factory

The Token Mill can only be used for new tokens.

Everything starts at the factory where the token is created, vesting schedules are set, parameters for the supply curve are set and the orderbook (or token market) is created.

The steps to create a new token are:

1. Create token
2. Create vesting schedule for locked tokens (token locker)
3. Create token market (bin-style orderbook)
4. Create supply curve/bonding curve (the market maker of last resort)
5. Send tokens to token locker, token market and supply curve
6. Transfer ownership for token and token locker
7. Commence dutch auction
8. Enable trading

This part requires a lot of configuration, which can get tedious, so we have provided several templates for you to choose from.

After the token is created, locked tokens are sent to the token locker where they will be vested according to the given schedule and the remaining tokens are sent to the supply curve.

<p align="center">
  <img src="/img/tm_components.png" alt="Different components of the Token Mill" width="800px" />
</p>
