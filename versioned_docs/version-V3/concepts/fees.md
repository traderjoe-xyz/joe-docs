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

Token Mill charges a fixed platform fee of 20%. If there is a referrer, they receive half of this fee (10%). The remaining 80% is allocated according to the creator's preference, which can be split between the creator and staking.

### Staking

Creators can choose to implement staking for their token, enabling fees to be distributed to stakers. Fees are streamed continuously and stakers can claim fees in real time. There is no lock up or vesting of staked tokens. However, locked tokens can also be staked.

### Referral Program

Creators have the option to include a referral program, allowing users to refer friends and earn a share of the fees from their trades ad infinitum.

Referrals apply to all markets and referrers get half of the platform fee (10%).
