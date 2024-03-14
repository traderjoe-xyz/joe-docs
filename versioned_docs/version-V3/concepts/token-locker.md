---
sidebar_position: 1
sidebar_label: Tokens & Token Locker
---

# Tokens and Token Locker

Tokens will be created from token templates.

The standard token template will be a basic ERC-20 with the following properties:
- Immmutable max supply
- No mint function / fully minted at creation
- Basic user inputs
    - Token owner address
    - Token symbol and name
    - Token decimals
    - Token supply
- 100% transferred either to the token market or the token locker
- Token Locker will have a minimum lock period on newly created tokens

The token locker is responsible for distribution, locking and vesting of token allocations for different stakeholders, e.g. team, investors, advisors, etc.

The locking and vesting schedule terms are set during token creation.
