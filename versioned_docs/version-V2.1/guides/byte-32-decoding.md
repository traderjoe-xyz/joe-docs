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
  const amountsBigInt = BigInt(
    `0x${Buffer.from(amounts, "hex").toString("hex")}`
  );

  // Read the right 128 bits of the 256 bits
  const amountsX = amountsBigInt & (BigInt(2) ** BigInt(128) - BigInt(1));

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
<TabItem value="flipside" label="Flipside SQL" default>

```sql
SELECT
  TX_HASH,
  BLOCK_TIMESTAMP,
  ethereum.public.udf_hex_to_int (SUBSTR(SUBSTR(DATA, 3 + 2 * 64, 64), 33, 32)) :: integer AS AMOUNT_X_OUT,
  ethereum.public.udf_hex_to_int (SUBSTR(SUBSTR(DATA, 3 + 2 * 64, 64), 1, 32)) :: integer as AMOUNT_Y_OUT,
FROM
  avalanche.core.fact_event_logs
WHERE
  TOPICS [0] = '0xad7d6f97abf51ce18e17a38f4d70e975be9c0708474987bb3e26ad21bd93ca70'
  AND CONTRACT_ADDRESS = LOWER('0xD446eb1660F766d533BeCeEf890Df7A69d26f7d1')
LIMIT
  100
```

</TabItem>
<TabItem value="dune" label="DUNE SQL" default>

```sql
SELECT
  tx_hash,
  block_time,
  bytearray_to_int256(bytearray_substring (DATA, 1 + 2 * 32 + 16, 16)) as AMOUNT_X_OUT,
  bytearray_to_int256(bytearray_substring (DATA, 1 + 2 * 32, 16)) as AMOUNT_Y_OUT
FROM
  avalanche_c.logs
WHERE
  topic0 = 0xad7d6f97abf51ce18e17a38f4d70e975be9c0708474987bb3e26ad21bd93ca70
  and contract_address = 0xD446eb1660F766d533BeCeEf890Df7A69d26f7d1
LIMIT
  100
```

</TabItem>
</Tabs>
