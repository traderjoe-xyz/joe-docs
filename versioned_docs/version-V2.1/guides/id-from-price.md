---
sidebar_position: 9
sidebar_label: Bin Id From Price
---

# Get Bin Id From Price

As mentioned previously, it is possible to link a `bin` to a price. It is also possible to perform the conversion in the other direction and thus link a price to a `bin`. We provide examples to get the `binId` from a price.

### Conversion Functions

As the previous example, it is necessary to know the `binStep` of the underlying pair. Here is the conversion logic.

```typescript
function getIdFromPrice(price: number, binStep: number): number {
  /**
   * Convert a price to the underlying binId.
   *
   * @param price - Price of the bin.
   * @param binStep - BinStep of the pair.
   * @return BinId of the underlying bin.
   */
  
    return (
      Math.trunc(Math.log(price) / Math.log(1 + binStep / 10_000)) + 8388608
    )
  }
```

```python
import math

def getIdFromPrice(price: float, binStep: int) -> int:
    """
    Convert a price to the underlying binId.

    :param price: Price of the bin.
    :param binStep: BinStep of the pair.
    :return: Id of the underlying bin.
    """
    
    return (
      math.trunc(math.log(price) / math.log(1 + binStep / 10_000)) + 8388608
    )
```

### Example

Here is an example to illustrate the conversion function with the [`sAVAX`/`AVAX`](https://traderjoexyz.com/avalanche/pool/v21/0x2b2c81e08f1af8835a78bb2a90ae924ace0ea4be/AVAX/5) pair which has a `binStep` of 5. We choose here a price equal to 1.075.

```python
getIdFromPrice(1.075, 5)
>>> 8388752
```
