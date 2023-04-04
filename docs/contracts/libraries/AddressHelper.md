## Address Helper

This library contains functions to check if an address is a contract and catch low level calls errors.

### callAndCatch

```solidity
function callAndCatch(address target, bytes memory data) internal returns (bytes memory)
```

Private view function to perform a low level call on `target`.

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| target | address | The address of the account |
| data | bytes | The data to execute on `target` |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| returnData | bytes | The data returned by the call |

### isContract

```solidity
function isContract(address account) internal view returns (bool)
```

Private view function to return if an address is a contract.

It is unsafe to assume that an address for which this function returns false is an externally-owned account (EOA) and not a contract.

Among others, `isContract` will return false for the following types of addresses:

- an externally-owned account
- a contract in construction
- an address where a contract will be created
- an address where a contract lived, but was destroyed

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| account | address | The address of the account |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| N/A | bool | Whether the account is a contract (true) or not (false) |