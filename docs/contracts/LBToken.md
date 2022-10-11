---
sidebar_position: 1
sidebar_label: LBToken
---

## LBToken

The LBToken is an implementation of a multi-token.
It allows to create multi-ERC20 represented by their ids

### name

```solidity
function name() public pure virtual override returns (string)
```

Returns the name of the token

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| [0] | string | The name of the token |

### symbol

```solidity
function symbol() public pure virtual override returns (string)
```

Returns the symbol of the token, usually a shorter version of the name

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| [0] | string | The symbol of the token |

### totalSupply

```solidity
function totalSupply(uint256 _id) public view virtual override returns (uint256)
```

Returns the total supply of token of type `id`

_This is the amount of token of type `id` minted minus the amount burned_

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _id | uint256 | The token id |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| [0] | uint256 | The total supply of that token id |

### balanceOf

```solidity
function balanceOf(address _account, uint256 _id) public view virtual override returns (uint256)
```

Returns the amount of tokens of type `id` owned by `_account`

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _account | address | The address of the owner |
| _id | uint256 | The token id |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| [0] | uint256 | The amount of tokens of type `id` owned by `_account` |

### balanceOfBatch

```solidity
function balanceOfBatch(address[] _accounts, uint256[] _ids) public view virtual override checkLength(_accounts.length, _ids.length) returns (uint256[] batchBalances)
```

Return the balance of multiple (account/id) pairs

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _accounts | address[] | The addresses of the owners |
| _ids | uint256[] | The token ids |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| batchBalances | uint256[] | The balance for each (account, id) pair |

### userPositionAtIndex

```solidity
function userPositionAtIndex(address _account, uint256 _index) public view virtual override returns (uint256)
```

Returns the type id at index `_index` where `account` has a non-zero balance

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _account | address | The address of the account |
| _index | uint256 | The position index |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| [0] | uint256 | The `account` non-zero position at index `_index` |

### userPositionNumber

```solidity
function userPositionNumber(address _account) public view virtual override returns (uint256)
```

Returns the number of non-zero balances of `account`

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _account | address | The address of the account |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| [0] | uint256 | The number of non-zero balances of `account` |

### isApprovedForAll

```solidity
function isApprovedForAll(address _owner, address _spender) public view virtual override returns (bool)
```

Returns true if `spender` is approved to transfer `_account`'s tokens

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _owner | address | The address of the owner |
| _spender | address | The address of the spender |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| [0] | bool | True if `spender` is approved to transfer `_account`'s tokens |

### setApprovalForAll

```solidity
function setApprovalForAll(address _spender, bool _approved) public virtual override 
```

Grants or revokes permission to `spender` to transfer the caller's tokens, according to `approved`

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _spender | address | The address of the spender |
| _approved | bool | The boolean value to grant or revoke permission |

### safeTransferFrom

```solidity
function safeTransferFrom(address _from, address _to, uint256 _id, uint256 _amount) public virtual override checkAddresses(_from, _to) checkApproval(_from, msg.sender)
```

Transfers `_amount` token of type `_id` from `_from` to `_to`

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _from | address | The address of the owner of the token |
| _to | address | The address of the recipient |
| _id | uint256 | The token id |
| _amount | uint256 | The amount to send |

### safeBatchTransferFrom

```solidity
function safeBatchTransferFrom(address _from, address _to, uint256[] _ids, uint256[] _amounts) public virtual override checkLength(_ids.length, _amounts.length) checkAddresses(_from, _to) checkApproval(_from, msg.sender)
```

Batch transfers `_amount` tokens of type `_id` from `_from` to `_to`

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _from | address | The address of the owner of the tokens |
| _to | address | The address of the recipient |
| _ids | uint256[] | The list of token ids |
| _amounts | uint256[] | The list of amounts to send |

### _transfer

```solidity
function _transfer(address _from, address _to, uint256 _id, uint256 _amount) internal virtual
```

Internal function to transfer `_amount` tokens of type `_id` from `_from` to `_to`

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _from | address | The address of the owner of the token |
| _to | address | The address of the recipient |
| _id | uint256 | The token id |
| _amount | uint256 | The amount to send |

### _mint

```solidity
function _mint(address _account, uint256 _id, uint256 _amount) internal virtual
```

_Creates `_amount` tokens of type `_id`, and assigns them to `_account`_

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _account | address | The address of the recipient |
| _id | uint256 | The token id |
| _amount | uint256 | The amount to mint |

### _burn

```solidity
function _burn(address _account, uint256 _id, uint256 _amount) internal virtual
```

_Destroys `_amount` tokens of type `_id` from `_account`_

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _account | address | The address of the owner |
| _id | uint256 | The token id |
| _amount | uint256 | The amount to destroy |

### _setApprovalForAll

```solidity
function _setApprovalForAll(address _owner, address _spender, bool _approved) internal virtual
```

Grants or revokes permission to `spender` to transfer the caller's tokens, according to `approved`

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _owner | address | The address of the owner |
| _spender | address | The address of the spender |
| _approved | bool | The boolean value to grant or revoke permission |

### _isApprovedForAll

```solidity
function _isApprovedForAll(address _owner, address _spender) internal view virtual returns (bool)
```

Returns true if `spender` is approved to transfer `owner`'s tokens
or if `sender` is the `owner`

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _owner | address | The address of the owner |
| _spender | address | The address of the spender |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| [0] | bool | True if `spender` is approved to transfer `owner`'s tokens |

### _add

```solidity
function _add(address _account, uint256 _id, uint256 _accountBalance, uint256 _amount) internal
```

Internal function to add an id to an user's set

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _account | address | The user's address |
| _id | uint256 | The id of the token |
| _accountBalance | uint256 | The user's balance |
| _amount | uint256 | The amount of tokens |

### _remove

```solidity
function _remove(address _account, uint256 _id, uint256 _accountBalance, uint256 _amount) internal
```

Internal function to remove an id from an user's set

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _account | address | The user's address |
| _id | uint256 | The id of the token |
| _accountBalance | uint256 | The user's balance |
| _amount | uint256 | The amount of tokens |

### _beforeTokenTransfer

```solidity
function _beforeTokenTransfer(address from, address to, uint256 id, uint256 amount) internal virtual
```

Hook that is called before any token transfer. This includes minting
and burning.

Calling conditions (for each `id` and `amount` pair):

- When `from` and `to` are both non-zero, `amount` of ``from``'s tokens
of token type `id` will be  transferred to `to`.
- When `from` is zero, `amount` tokens of token type `id` will be minted
for `to`.
- when `to` is zero, `amount` of ``from``'s tokens of token type `id`
will be burned.
- `from` and `to` are never both zero.

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| from | address | The address of the owner of the token |
| to | address | The address of the recipient of the  token |
| id | uint256 | The id of the token |
| amount | uint256 | The amount of token of type `id` |

