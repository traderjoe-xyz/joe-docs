## LBToken

The LBToken is an implementation of a multi-token. It allows creating multi-ERC20 represented by their ids. Its implementation is similar to the ERC1155 standard, the main difference being that it doesn't do any call to the receiver contract to prevent reentrancy. As it's only for ERC20s, the uri function is not implemented. The contract is made for batch operations.

### name

```solidity
function name() public view virtual override returns (string memory)
```

Returns the name of the token.

#### Return Value

| Name | Type | Description |
| ---- | ---- | ----------- |
|     | string | The name of the token. |

### symbol

```solidity
function symbol() public view virtual override returns (string memory)
```

Returns the symbol of the token, usually a shorter version of the name.

#### Return Value

| Name | Type | Description |
| ---- | ---- | ----------- |
|     | string | The symbol of the token. |

### totalSupply

```solidity
function totalSupply(uint256 id) public view virtual override returns (uint256)
```

Returns the total supply of token of type `id`. This is the amount of token of type `id` minted minus the amount burned.

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| `id` | uint256 | The token id. |

#### Return Value

| Name | Type | Description |
| ---- | ---- | ----------- |
|     | uint256 | The total supply of that token id. |

### balanceOf

```solidity
function balanceOf(address account, uint256 id) public view virtual override returns (uint256)
```

Returns the amount of tokens of type `id` owned by `account`.

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| `account` | address | The address of the owner. |
| `id` | uint256 | The token id. |

#### Return Value

| Name | Type | Description |
| ---- | ---- | ----------- |
|     | uint256 | The amount of tokens of type `id` owned by `account`. |

### balanceOfBatch

```solidity
function balanceOfBatch(address[] memory accounts, uint256[] memory ids) public view virtual override checkLength(accounts.length, ids.length) returns (uint256[] memory batchBalances)
```

Returns the balance of multiple (account/id) pairs.

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| `accounts` | address[] | The addresses of the owners. |
| `ids` | uint256[] | The token ids. |

#### Return Value

| Name | Type | Description |
| ---- | ---- | ----------- |
|    | uint256[] | The balance for each (account, id) pair. |

### isApprovedForAll

```solidity
function isApprovedForAll(address owner, address spender) public view virtual override returns (bool)
```

Returns true if `spender` is approved to transfer `account`'s tokens.

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| `owner` | address | The address of the owner. |
| `spender` | address | The address of the spender. |

#### Return Value

| Name | Type | Description |
| ---- | ---- | ----------- |
|     | bool | True if `spender` is approved to transfer `account`'s tokens. |

### approveForAll

```solidity
function approveForAll(address spender, bool approved) public virtual override
```

Grants or revokes permission to `spender` to transfer the caller's lbTokens, according to `approved`.

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| `spender` | address | The address of the spender. |
| `approved` | bool | The boolean value to grant or revoke permission. |

### batchTransferFrom

```solidity
function batchTransferFrom(address from, address to, uint256[] memory ids, uint256[] memory amounts) public virtual override checkApproval(from, msg.sender)
```

Batch transfers `amounts` of `ids` from `from` to `to`.

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| `from` | address | The address of the owner. |
| `to` | address | The address of the recipient. |
| `ids` | uint256[] | The list of token ids. |
| `amounts` | uint256[] | The list of amounts to transfer for each token id in `ids`. |

### _isApprovedForAll

```solidity
function _isApprovedForAll(address owner, address spender) internal view returns (bool)
```

Returns true if `spender` is approved to transfer `owner`'s tokens or if `sender` is the `owner`.

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| owner | address | The address of the owner |
| spender | address | The address of the spender |


#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| bool | bool | True if `spender` is approved to transfer `owner`'s tokens. |

### _mintBatch

```solidity
function _mintBatch(address account, uint256[] memory ids, uint256[] memory amounts) internal notAddressZeroOrThis(account) checkLength(ids.length, amounts.length)
```

Batch mints `amounts` of `ids` to `account`. The `account` must not be the zero address and the `ids` and `amounts` must have the same length.


#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| account | address | The address of the owner |
| ids | uint256[] | The list of token ids |
| amounts | uint256[] | The list of amounts to mint for each token id in `ids` |


### _burnBatch

```solidity
function _burnBatch(address account, uint256[] memory ids, uint256[] memory amounts) internal notAddressZeroOrThis(account) checkLength(ids.length, amounts.length)
```

Batch burns `amounts` of `ids` from `account`. The `ids` and `amounts` must have the same length.

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| account | address | The address of the owner |
| ids | uint256[] | The list of token ids |
| amounts | uint256[] | The list of amounts to burn for each token id in `ids` |

### _batchTransferFrom

```solidity
function _batchTransferFrom(address from, address to, uint256[] memory ids, uint256[] memory amounts) internal checkLength(ids.length, amounts.length) notAddressZeroOrThis(to)
```

Batch transfers `amounts` of `ids` from `from` to `to`. The `to` must not be the zero address and the `ids` and `amounts` must have the same length.

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| from | address | The address of the owner |
| to | address | The address of the recipient |
| ids | uint256[] | The list of token ids |
| amounts | uint256[] | The list of amounts to transfer for each token id in `ids` |

### _approveForAll

```solidity
function _approveForAll(address owner, address spender, bool approved) internal
```

Grants or revokes permission to `spender` to transfer the caller's tokens, according to `approved`

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| owner | address | The address of the owner |
| spender | address | The address of the spender |
| approved | bool | The boolean value to grant or revoke permission |