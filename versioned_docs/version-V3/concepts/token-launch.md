---
sidebar_position: 2
sidebar_label: Token Launch
---

# Token Launch

The initial token launch is done via dutch auction.

Creators can choose from a set of auction templates. Each template will specify a start and end time for each auction.

Token auction begins with a bidding phase and ends with tokens being released from the supply curve to fill the bids. 

After token auction is over, trading is enabled.

## Bidding Phase

Auction starts with participants placing bids in bins at the price they would be willing to exchange for the token.

Bin withdrawals is gradually restricted over the course of the auction, starting from highest price to lowest price, until the auction is over.

Once a bin is locked, the bids remain there until the auction concludes.

<p align="center">
  <img src="/img/auction_bidding.png" alt="Auction bidding" width="400px" />
</p>

## Supply Curve Settlement

Once the auction has concluded, tokens supplied to the supply curve (or bonding curve) will settle against the participants' bids.

All bids will be filled provided there is liquidity available from the supply curve.

Starting from the highest bid, bins are filled from the supply curve as long as the supply curve has a lower price than the bid price.

Using the example in figures 8 and 9, bins with prices of 57, 56, and 55 will receive 90 tokens (20+30+40). The next group of bids is at P=54 worth 40 tokens, but the supply curve only has 10 remaining tokens to issue until it also has a price of 54. 10 tokens will be sent to bin 54 and depositors to that bin would be partially filled.

<p align="center">
  <img src="/img/auction_settlement.png" alt="Auction bidding" width="800px" />
</p>

## Open Trading

Following settlement, withdrawals are enabled and participants may claim their tokens from the auction. The market is then open for trading and the highest bin with unfilled bids from the auction becomes the active bin.

<p align="center">
  <img src="/img/auction_finish.png" alt="Auction bidding" width="400px" />
</p>
