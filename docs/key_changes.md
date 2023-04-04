---
sidebar_position: 1
sidebar_label: V2.1 Key Changes
---

# V2.1 Key Changes

A summary of key changes in Liquidity Book V2.1: 
- `LBPair` presets.
- Gas optimization with swap amount encoding.
- Limit orders.
- Router and quoter support across all versions.

### LBFactory

In this contract the changes are mainly linked to preset updates:
- The `uint256 sampleLifetime` parameter has been removed from the `PresetSet` event.
- The `getPreset()` function now return an additional parameter, `bool isOpen`, that tracks if the change of preset is open or not. The `sampleLifetime` variable has been removed.
- When `isOpen` is updated, a new event, 'PresetOpenStateChanged', is emitted.
- Additionally, the `MAX_FEE()`, `MIN_BIN_STEP()`, `MAX_BIN_STEP()` and `MAX_PROTOCOL_SHARE()` functions have been removed.
- The following new functions have been added: `getMinBinStep()`, `getFeeRecipient()`, `getMaxFlashLoanFee()`, `getFlashLoanFee()` and `getLBPairImplementation()`.

### LBPair 

- The event `FeeParametersSet` has been removed from `LBFactory` and a new event `StaticFeeParametersSet` has been added to LBPair instead.
- Several parameters from the following events have been changed from `uint256` to `bytes32`: `DepositedToBins`, `WithdrawnFromBins`, `CompositionFees`, `CollectedProtocolFees`, `Swap` and `FlashLoan`. To decode, see [decode examples](guides/decode-examples).
- Several parameters from the following functions have been changed from `uint256` to `bytes32`: `swap()`, `flashLoan()`, `mint()`, `burn()` and `collectProtocolFees()`. To decode, see [decode examples](guides/decode-examples).
-The `getReservesAndId()` function has been deprecated and replaced by two new functions: `getReserves()` and `getActiveId()`.
- The following new functions have been added: `getNextNonEmptyBin()`, `getProtocolFees()`, `getStaticFeeParameters()` and `getVariableFeeParameters()`.

### LBRouter 

The router now support quotes for V1, V2 and V2.1 pairs.
- An enum, `Version`, has been added to specify the version of the pair that the route will be swapped through.
- A new struct, `Path`, has been added that represents the pairs that route passes through, where each pair is uniquely identified by `(tokenX, tokenY, version, pairBinStep)` (`pairBinStep` for V1 pairs is 0).
- A new parameter, `refundTo`, has been added to the `LiquidityParameters` struct that specifies which address to refund excess tokens to when new liquidity positions are minted.
- All naming references of `AVAX` have been replaced with `NATIVE`.
    - E.g. `swapExactTokensForAVAX()` is now `swapExactTokensForNATIVE()`.
- Swap, add and remove liquidity functions now use new Path struct as input.

### LBToken

- The functions `safeTransferFrom()` and `safeBatchTransferFrom()` have been replaced by `batchTransferFrom()`.

### LBQuoter

The new quoter now support quotes from all pair versions.
