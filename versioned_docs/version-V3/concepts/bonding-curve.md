---
sidebar_position: 3
sidebar_label: Bonding Curve
---

# Bonding Curve

The AMM portion of the hybrid AMM/orderbook design is the bonding curve, where tokens are priced according to a creator-defined price-supply curve.

This is the same kind of bonding curve popularized by the socialFi app, FriendTech. However, in Token Mill creators can define their own pricing function according to the inputted parameters and there are separate curves for bids and asks.

## Terminology

The whitepaper defines a few variables, which are important to understand before we dive into the paramterization of the supply curve.

$S_T$ is the total max supply of the token.

$s$ is supply supplied to the supply curve/bonding curve pool.

$x$ is the amount of tokens bought from the supply curve pool (and is now in circulation).

$r$ is the amount of tokens available to be released from the token locker.

Example: Token XYZ has 1B supply cap. On initialization, 800M is put into the supply curve pool. After 1 month, 50M tokens are released to the team. Later, 200M is bought by market participants.

$S_T$ = 1B, $s$ = 800M, $x$ = 200M, $r$ = 50M.

Circulating tokens = 250M, pool issued tokens = 200M and the supply curve pool only has funds to buy back 200M of 250MM outstanding.

## Price and Capacity

The price of any token is defined by a quadratic: $P(x) = Ax^2 + Bx + P_0$.

When a token is created, the creator defines 4 variables:

- Total supply to the pool, $s$
- Minimum price of the curve, $P_0$ (or $c$ of the quadratic formula)
- Maximum price of the curve, $P_max$
- Max capacity, $C_{max}$ (note: different to $c$ of the quadratic formula!)

The remaining unknown variables, $A$ and $B$, are then calculated from these inputted parameters.

### Capacity

The capacity, $C$, is the amount of capital that can absorb the amount of tokens sold by the supply curve pool. In the above example, it would be the amount of USDC that can absorb all 200M XYZ tokens if they were sold back to the supply curve pool.

The _max capacity_, $C_{max}$, is therefore the total amount of capital that can absorb the entire supply of the pool, $s$.

This variable is defined by the creator at token creation. An easier way to think about it is the amount of USDC the creator wants to raise for issuing $s$ amount of XYZ tokens.

For example, if Alice supplies 800M XYZ tokens and wants to raise 50M USDC. $C_{max}$ would therefore be 50M.

Mathematically, $C_{max}$ is the integral of the price function of all tokens in the supply curve:

$$
C_{max} = \int_{0}^{s} P(x)
$$

$P(x)$ is a quadratic, so $C_{max}$ can be rewritten as:

$$
C_{max} = \int_{0}^{s} Ax^2 + Bx + P_0 \\
C_{max} = \left[ \frac{Ax^3}{3} + \frac{Bx^2}{2} + P_0x \right]_0^s
$$

And since the creator defines $C_{max}$, $s$, and $P_0$, we can solve to find the remaining unknown variables, $A$ and $B$, to dedude the pricing formula of the supply curve.

## Defining Your Bonding Curve

The token creator only needs to define the above 4 variables.

They would simply ask themselves: how much capital do I want to raise ($C_{max}$) in exchange for how many tokens ($s$) within what price range ($P_0 - P_s$)?

We are then able to find the 2 unknown variables of the pricing function, $A$ and $B$, using those 4 variables (math can be found in the whitepaper).

Below is an example pricing curve from the whitepaper, given the 4 user-defined inputs.

$V_L = P_0 * s$ is the minimum FDV of the supply curve pool.

$V_H = P_s * s$ is the maximum FDV of the supply curve pool.

<p align="center">
  <img src="/img/example_supply_curve.png" alt="Example supply curve" width="800px" />
</p>

## Bid & Ask Curves

During the token launch phase, tokens are issued to auction participants according to the ask curve.

Once secondary market phase commences, tokens are traded along two separate curves:

- Bid curve from which tokens are bought
- Ask curve from which tokens are sold

The ask curve has the same quadratic pricing formula defined previously, but the pricing function for the bid curve is scaled down by a factor $$\alpha$$, such that $$0 < \alpha < 1$$ and $$P_{bid}(x) < P_{ask}(x)$$ for all $$x$$ in $$[0,s]$$.

$$
P_{ask} = Ax^2 + Bx + P_0\\
P_{bid} = \alpha(Ax^2 + Bx +P_0)
$$

At any point in supply, the bid and ask price will always be different and the spread therefore represents the fee collected.

<p align="center">
  <img src="/img/bid_ask_curves.png" alt="Bid ask curves" width="600px" />
</p>

## Bonding Curve Initialization

The ask curve pool will contain only the base token (e.g. XYZ) and the bid curve will be empty.

After the token auction concludes however, the bid curve will contain enough quote token (e.g. USDC) to absorb any tokens issued (minus tokens released by the token locker) -- this is the capacity.

Once initalized, it acts as a liquidity pool where market participants can buy or sell tokens into without any need for external liquidity providers.
