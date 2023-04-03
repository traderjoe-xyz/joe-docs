---
sidebar_position: 2
sidebar_label: Decode Examples
---

# How To Decode Bytes Parameters

Some of the new function and event variables are packed and encoded in `bytes32`. To read them, they will need to be decoded. Below we explain how.

## Decode `amountsIn` or `amountsOut` from the `Swap` event

The parameter `amountsIn` is packed with the amounts in for both tokens X and Y and encoded into `bytes32`. Below is an example of how to decode them. The same is true for `amountsOut`.

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

### Decode `totalFees` and `protocolFees` from `Swap` Event

The following functions return the decoded values of the Fees of the `LBPair` contract.

```typescript
function decodeFees(feesBytes: Bytes): bigint {
  /**
   * Decode the fee value from the bytes input and return it as in integer.
   * Fee values are stored in the first 128 bits of the input.
   *
   * @param feesBytes - Bytes containing the encoded value.
   * @return Fee values.
   */

  // Convert feesBytes to a BigInt
  const feesBigInt = BigInt(`0x${Buffer.from(feesBytes).toString('hex')}`);

  // Retrieve the fee value from the right 128 bits
  return feesBigInt & ((BigInt(2) ** BigInt(128)) - BigInt(1));
}
```

```python
def decodeFees(fees_bytes: bytes) -> int:
    """
    Decode the fee value from the bytes input and return it as in integer.
    Fee values are stored in the first 128bits ofthe input.

    :param fees_bytes: Bytes containing the encoded value.
    :return: Fee values.
    """

    fees_bytes = bytes.fromhex(fees_bytes)
    
    # Retrieve the fee value from the right 128 bits
    return int.from_bytes(fees_bytes, byteorder="big") & (2 ** 128 - 1)
```