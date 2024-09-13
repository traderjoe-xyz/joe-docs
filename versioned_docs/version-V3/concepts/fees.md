---
sidebar_position: 3
sidebar_label: Fees
---

# Fees

## Purchase Fees

Token Mill has a single fee: a fee charged only when tokens are bought and is defined as the spread between the ask price and bid price.

When a token is bought, user pays the ask price $$P_{ask}(x)$$. The fee is distributed to the beneficiaries and an amount equal to the bid price $$P_{bid}(x)$$ is sent to the bonding curve to absorb any sales back to the curve.

Because the fee is determined by the spread between the bid and ask prices, you can technically apply different fees at various price points. However, to simplify the process, Token Mill offers the option to set a fixed fee.

## Customize Fees

Token Mill allows you to customize the allocation of fees among various beneficiaries.

There are four beneficiaries that can receive a portion of the purchase fee:
- Protocol (Token Mill)
- Creator 
- Staking
- Referral

Token Mill charges a fixed platform fee of 20%. The creator has full flexibility in distributing the remaining 80% as desired.

### Staking

Creators can choose to implement staking for their token, enabling fees to be distributed to stakers.

### Referrals

Creators have the option to include a referral program, allowing users to refer friends and earn a share of the fees from their trades.

Users without a referrer will have this portion of the fee disributed to the beneficiaries.

### Example

Creator sets the fees to:
- Protocol 20%
- Creator 20%
- Staking 40%
- Referral 20%

If a user buys a token without a referrer, then the fee becomes protocol 25%, creator 25% and staking 50%.
