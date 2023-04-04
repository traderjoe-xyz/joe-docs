---
sidebar_position: 2
sidebar_label: Tracking Volume
---


# Tracking Volume

:::note
#### Key Changes in V2.1
- `LBFactory.LBPairCreated` event has additional `pid` pool Id which is unique for a single pool in a factory. 
- `LBPair.Swap` event returns `amountsIn` and `amountsOut` encoded `bytes32` instead of `uint256`. See [decode examples](guides/decode-examples) for more.
:::

Each market has its own `LBPair` contract with its own address. These are created by the `LBFactory` contract. 

The general approach is to track all `LBPairs` created by the `LBFactory` and then track all `Swap` events emitted by the `LBPair`. 


## LBPairCreated

The `LBPairCreated` event is emitted by the `LBFactory` when new `LBPair` is created. Pools are uniquely identified within factories by `pid`.

```
    // ILBFactory.sol
    event LBPairCreated(
        IERC20 indexed tokenX, 
        IERC20 indexed tokenY, 
        uint256 indexed binStep, 
        ILBPair LBPair, 
        uint256 pid
    );
```

Below is code example to extract the `LBPair`, `tokenX`, `tokenY` addresses, `pid`, and `binstep`. 

```typescript
function handleLBPairCreated(event: LBPairCreated): void {

  const lbPair = new LBPair(
    event.params.pid,
    event.params.LBPair.toHexString(), 
    event.params.tokenX.toHexString(), 
    event.params.tokenY.toHexString(), 
    event.params.binStep
  )

  lbPair.save()
}
```


## Swap

The `Swap` event is emitted by `LBPairs` when tokens are swapped.  
- Volume traded is tracked by `amountsIn`, `amountsOut`, which are tuple `[amountX, amountY]` encoded into `byte32`. 
- Fees paid by Traders to Liquidity Providers are tracked in `totalFees`, while fees paid by Liquidity Providers to Protocol are tracked in `protocolFees`. They are tuple `[feeX, feeY]` encoded into `byte32`. 
- See [Decode Example](./decode-examples.md) for more details. 
- The active bin when the swap has finished is tracked by `id`, which is the Bin ID in integer. 


````
    // ILBPair.sol
    event Swap(
        address indexed sender,
        address indexed to,
        uint24 id,
        bytes32 amountsIn,
        bytes32 amountsOut,
        uint24 volatilityAccumulator,
        bytes32 totalFees,
        bytes32 protocolFees
    );
````

Below are code example to get the price, and amounts swapped. 

```typescript
export function handleSwap(event: Swap): void {

  // We can get the tokenX and tokenY from the LBPair
  const lbPair = LBPair.load(event.address.toHexString())
  const tokenX = lbPair.tokenX
  const tokenY = lbPair.tokenY

  // We can infer the price of 1 tokenY = __ tokenX 
  // from the binstep and the active Bin Id
  const price = getPriceOfBin(
    BigInt.fromString(event.params.id.toString()),
    lbPair.binStep,
    tokenX,
    tokenY
  )

  // NOTE: reverse bytes to convert to big endianness
  event.params.amountsIn.reverse()
  event.params.amountsOut.reverse()

  // amountsIn is [amountX, amountY] packed into byte32
  const amountInX = decodeX(event.params.amountsIn)
  const amountInY = decodeY(event.params.amountsIn)
  const amountOutX = decodeX(event.params.amountsOut)
  const amountOutY = decodeY(event.params.amountsOut)

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
