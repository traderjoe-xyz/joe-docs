---
sidebar_position: 8
sidebar_label: Price From Bin Id
---

# Get Price From Bin Id

In v2.1 each `bin` holds the liquidity of the pair for a specific price range. Thus, it is possible to link a certain `bin` to a price by using the `id` of the underlying `bin`. We provide examples to get the price from a `binId`.

### Conversion Functions

In order to link a `binId` to a price it is necessary to know the `binStep` of the underlying pair. Here is the conversion logic.

```typescript
function getPriceFromId(binId: number, binStep: number): number {
  /**
   * Convert a binId to the underlying price.
   *
   * @param binId - Bin Id.
   * @param binStep - binStep of the pair.
   * @return Price of the bin.
   */

    return (1 + binStep / 10_000) ** (binId - 8388608);
  }
```

```python
def getPriceFromId(binId: int, binStep: int) -> float:
    """
    Convert a binId to the underlying price.

    :param binId: Bin Id.
    :param binStep: BinStep of the pair.
    :return: Price of the bin.
    """

    return (1 + binStep / 10_000) ** (binId - 8388608)
```

### Example

Here is an example to illustrate the conversion function with the [`sAVAX`/`AVAX`](https://traderjoexyz.com/avalanche/pool/v21/0x2b2c81e08f1af8835a78bb2a90ae924ace0ea4be/AVAX/5) pair which has a `binStep` of 5. We choose here a `binId` equal to 8388755.

```python
getPriceFromId(8388755, 5)
>>> 1.0762487670087693
```
