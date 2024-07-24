---
sidebar_position: 8
sidebar_label: Price From Bin Id
---

import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

# Get Price From Bin Id

In v2.2 each `bin` holds the liquidity of the pair for a specific price range. Thus, it is possible to link a certain `bin` to a price by using the `id` of the underlying `bin`. We provide examples to get the price from a `binId`.

### Conversion Functions

In order to link a `binId` to a price it is necessary to know the `binStep` of the underlying pair. Here is the conversion logic.
<Tabs>
<TabItem value="typescript" label="Typescript">

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

</TabItem>
<TabItem value="python" label="Python" default>

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

</TabItem>
</Tabs>

### Example

Here is an example to illustrate the conversion function with the [`sAVAX`/`AVAX`](https://traderjoexyz.com/avalanche/pool/v22/0x2b2c81e08f1af8835a78bb2a90ae924ace0ea4be/AVAX/5) pair which has a `binStep` of 5. We choose here a `binId` equal to 8388755. Price returned doesn't need to be adjusted, as both tokens have 18 decimals.

```python
getPriceFromId(8388755, 5)
>>> 1.0762487670087693
```

For second example, let's take [BTC.b/USDC](https://traderjoexyz.com/avalanche/pool/v21/0x152b9d0fdc40c096757f570a51e494bd4b943e50/0xb97ef9ef8734c71904d8002f8b6bc66dd9c48a6e/10) pair which has a `binStep` of 10. We choose `binId` equal to 8394314.

```python
getPriceFromId(8394314, 10)
>>> 299.80998797504674
```

$$
priceAdjusted = price\cdot 10^{(\text{decimalsX} - \text{decimalsY})}
$$

$$
priceAdjusted = 299.80 \cdot 10^{(\text{8} - \text{6})} = 29800
$$
