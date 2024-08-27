---
sidebar_position: 7
sidebar_label: Bytes32 Decoding
---

import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

# Byte32 Decoding

In v2.1 we introduced `byte32` encoding for function and event variables (to save storage and gas costs). We provide examples to decode them. 


Many parameters (like `amountsIn`, `totalFees` in Swap event) are packed with the amounts in for both tokens X and Y and encoded into `bytes32`. Below is an example of how to decode them.


<Tabs>
<TabItem value="typescript" label="Typescript">

```typescript
function decodeAmounts(amounts: Bytes): [bigint, bigint] {
  /**
   * Decodes the amounts bytes input as 2 integers.
   *
   * @param amounts - amounts to decode.
   * @return tuple of BigInts with the values decoded.
   */

  // Convert amounts to a BigInt
  const amountsBigInt = BigInt(`0x${Buffer.from(amounts).toString('hex')}`);

  // Read the right 128 bits of the 256 bits
  const amountsX = amountsBigInt & ((BigInt(2) ** BigInt(128)) - BigInt(1));

  // Read the left 128 bits of the 256 bits
  const amountsY = amountsBigInt >> BigInt(128);

  return [amountsX, amountsY];
}
```

</TabItem>
<TabItem value="python" label="Python" default>

```python
def decodeAmounts(amounts: bytes) -> tuple:
    """
    Decodes the amounts bytes input as 2 integers.

    :param amounts: amounts to decode.
    :return: tuple of ints with the values decoded.
    """
    
    amounts = bytes.fromhex(amounts)

    # Read the right 128 bits of the 256 bits
    amountsX = int.from_bytes(random_bytes, byteorder="big") & (2 ** 128 - 1)

    # Read the left 128 bits of the 256 bits
    amountsY = int.from_bytes(random_bytes, byteorder="big") >> 128

    return (amountsX, amountsY)
```

</TabItem>
</Tabs>