---
sidebar_position: 2
sidebar_label: Decode Examples
---

## Decode Bytes Examples

Some of the new output variables from `functions` and `event` of the new `v2.1 Dex` needs to be decoded. Here are some propositions in order to do so: <br/>

### Decode `amountsOut` from the `Swap` event

The following functions return the decoded values (x, y) extracted from the encoded `bytes32` amounts. The functions are returning the results in a `tuple`.

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

  // Read the first 128 bits of the 256 bits
  const amountsX = amountsBigInt & ((BigInt(2) ** BigInt(128)) - BigInt(1));

  // Read the last 128 bits of the 256 bits
  const amountsY = amountsBigInt >> BigInt(128);

  return [amountsX, amountsY];
}
```

```python
def decodeAmounts(amounts: bytes) -> tuple:
    """
    Decodes the amounts bytes input as 2 integers.

    :param amounts: amounts to decode.
    :return: tuple of ints with the values decoded.
    """
    amounts = bytes.fromhex(amounts)
    # read the first 128bits of the 256bits
    amountsX = int.from_bytes(random_bytes, byteorder="big") & (2 ** 128 - 1)
    # read the last 128bits of the 256bits
    amountsY = int.from_bytes(random_bytes, byteorder="big") >> 128
    return (amountsX, amountsY)
```

### Decode `totalFees` and `protocolFees` from `Swap` Event

The following functions return the decoded values of the Fees of the `LBPair` contract.

```typescript
function decodeFees(feesBytes: Bytes): bigint {
  /**
   * Decode the Fee value from the bytes input and return it into a BigInt.
   * Fee values are stored in the first 128 bits of the input.
   *
   * @param feesBytes - Bytes containing the encoded value.
   * @return Fee values.
   */
  // Convert feesBytes to a BigInt
  const feesBigInt = BigInt(`0x${Buffer.from(feesBytes).toString('hex')}`);

  // Retrieve the fee value from the first 128 bits
  return feesBigInt & ((BigInt(2) ** BigInt(128)) - BigInt(1));
}
```

```python
def decodeFees(fees_bytes: bytes) -> int:
    """
    Decode the Fee value from the bytes input and return it into an int.
    Fee values are stored in the first 128bits ofthe input.

    :param fees_bytes: Bytes containing the encoded value.
    :return: Fee values.
    """
    fees_bytes = bytes.fromhex(fees_bytes)
    return int.from_bytes(fees_bytes, byteorder="big") & (2 ** 128 - 1)
```