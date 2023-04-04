---
sidebar_position: 3
sidebar_label: Tracking Pool Balances
---


# Tracking Pool Balances

:::note
#### Key Changes in V2.1

- Events `LiquidityAdded` and `LiquidityRemoved` are now replaced with `DepositedToBins` and `WithdrawnFromBins`. 
- Token amounts are now encoded in `byte32`. 
:::

The `LBPair` contract emits `DepositedToBins` and `WithdrawnFromBins` events when users add or remove liquidity from the market. 

We track the user balances in `LBPairs` by parsing these events. 
- Liquidity is deposited/withdrawn into multiple `Bins`, for which the `Bin Ids` are returned in array `uint256[] ids`. 
- Token amounts deposited/withdrawn are tracked by `amounts`, which is a of tuple `[amountX, amountY]` encoded into `byte32`. 
- The arrays `amounts[]` and `ids[]` correspond to the token amounts and `Bin Ids` of each corresponding `Bin`. 
- See [Decode Example](./decode-examples.md) for more details. 


## DepositedToBins

```solidity
    // ILBPair.sol
    event DepositedToBins(
      address indexed sender, 
      address indexed to, 
      uint256[] ids, 
      bytes32[] amounts
    );
```

## WithdrawnFromBins

```solidity
    // ILBPair.sol
    event WithdrawnFromBins(
      address indexed sender, 
      address indexed to, 
      uint256[] ids, 
      bytes32[] amounts
    );
```

## Example Handler

```typescript
export function handleDepositedToBins(event: DepositedToBins): void {

  // We can get the tokenX and tokenY from the LBPair
  const lbPair = LBPair.load(event.address.toHexString())
  const tokenX = lbPair.tokenX
  const tokenY = lbPair.tokenY

  // get user
  const user = User.load(event.to.toHexString())

  // get amounts
  const amounts = event.params.amounts
  let amountX = 0
  let amountY = 0
  for (let i=0; i < amounts.length; i++) {
    const _amounts = amounts[i]
    // NOTE: reverse bytes to convert to big endianness
    amounts.reverse()
    const _amountX = decodeX(_amounts)
    const _amountY = decodeY(_amounts)
    amountX += _amountX
    amountY += _amountY
  }
}

// Assemblyscript API
// https://thegraph.com/docs/en/developing/assemblyscript-api/
function decodeX(packedAmounts: Bytes): BigInt {
  // Read the right 128 bits of the 256 bits
  return BigInt.fromUnsignedBytes(packedAmounts).bitAnd(BigInt.fromI32(2).pow(128).minus(BigInt.fromI32(1)))
}

function decodeY(packedAmounts: Bytes): BigInt {
  // Read the left 128 bits of the 256 bits
  return BigInt.fromUnsignedBytes(packedAmounts).rightShift(128)
}

```


