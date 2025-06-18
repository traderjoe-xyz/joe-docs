# LBToken
[Git Source](https://github.com/lfj-gg/joe-v2/blob/16f011d25e6bf6d0a0c479974345b623d491104f/src/LBToken.sol)

**Inherits:**
[ILBToken](./interfaces/ILBToken.md)

**Author:**
Trader Joe

The LBToken is an implementation of a multi-token.
It allows to create multi-ERC20 represented by their ids.
Its implementation is really similar to the ERC1155 standard the main difference
is that it doesn't do any call to the receiver contract to prevent reentrancy.
As it's only for ERC20s, the uri function is not implemented.
The contract is made for batch operations.


## State Variables
### _balances
*The mapping from account to token id to account balance.*


```solidity
mapping(address => mapping(uint256 => uint256)) private _balances;
```


### _totalSupplies
*The mapping from token id to total supply.*


```solidity
mapping(uint256 => uint256) private _totalSupplies;
```


### _spenderApprovals
*Mapping from account to spender approvals.*


```solidity
mapping(address => mapping(address => bool)) private _spenderApprovals;
```


## Functions
### checkApproval

*Modifier to check if the spender is approved for all.*


```solidity
modifier checkApproval(address from, address spender);
```

### notAddressZeroOrThis

*Modifier to check if the address is not zero or the contract itself.*


```solidity
modifier notAddressZeroOrThis(address account);
```

### checkLength

*Modifier to check if the length of the arrays are equal.*


```solidity
modifier checkLength(uint256 lengthA, uint256 lengthB);
```

### name

Returns the name of the token.


```solidity
function name() public view virtual override returns (string memory);
```
**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`string`|The name of the token.|


### symbol

Returns the symbol of the token, usually a shorter version of the name.


```solidity
function symbol() public view virtual override returns (string memory);
```
**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`string`|The symbol of the token.|


### totalSupply

Returns the total supply of token of type `id`.
/**

*This is the amount of token of type `id` minted minus the amount burned.*


```solidity
function totalSupply(uint256 id) public view virtual override returns (uint256);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`id`|`uint256`|The token id.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint256`|The total supply of that token id.|


### balanceOf

Returns the amount of tokens of type `id` owned by `account`.


```solidity
function balanceOf(address account, uint256 id) public view virtual override returns (uint256);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`account`|`address`|The address of the owner.|
|`id`|`uint256`|The token id.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint256`|The amount of tokens of type `id` owned by `account`.|


### balanceOfBatch

Return the balance of multiple (account/id) pairs.


```solidity
function balanceOfBatch(address[] calldata accounts, uint256[] calldata ids)
    public
    view
    virtual
    override
    checkLength(accounts.length, ids.length)
    returns (uint256[] memory batchBalances);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`accounts`|`address[]`|The addresses of the owners.|
|`ids`|`uint256[]`|The token ids.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`batchBalances`|`uint256[]`|The balance for each (account, id) pair.|


### isApprovedForAll

Returns true if `spender` is approved to transfer `owner`'s tokens or if `spender` is the `owner`.


```solidity
function isApprovedForAll(address owner, address spender) public view virtual override returns (bool);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`owner`|`address`|The address of the owner.|
|`spender`|`address`|The address of the spender.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bool`|True if `spender` is approved to transfer `owner`'s tokens.|


### approveForAll

Grants or revokes permission to `spender` to transfer the caller's lbTokens, according to `approved`.


```solidity
function approveForAll(address spender, bool approved) public virtual override;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`spender`|`address`|The address of the spender.|
|`approved`|`bool`|The boolean value to grant or revoke permission.|


### batchTransferFrom

Batch transfers `amounts` of `ids` from `from` to `to`.


```solidity
function batchTransferFrom(address from, address to, uint256[] calldata ids, uint256[] calldata amounts)
    public
    virtual
    override
    checkApproval(from, msg.sender);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`from`|`address`|The address of the owner.|
|`to`|`address`|The address of the recipient.|
|`ids`|`uint256[]`|The list of token ids.|
|`amounts`|`uint256[]`|The list of amounts to transfer for each token id in `ids`.|


### _isApprovedForAll

Returns true if `spender` is approved to transfer `owner`'s tokens or if `spender` is the `owner`.


```solidity
function _isApprovedForAll(address owner, address spender) internal view returns (bool);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`owner`|`address`|The address of the owner.|
|`spender`|`address`|The address of the spender.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bool`|True if `spender` is approved to transfer `owner`'s tokens.|


### _mint

*Mint `amount` of `id` to `account`.
The `account` must not be the zero address.
The event should be emitted by the contract that inherits this contract.*


```solidity
function _mint(address account, uint256 id, uint256 amount) internal;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`account`|`address`|The address of the owner.|
|`id`|`uint256`|The token id.|
|`amount`|`uint256`|The amount to mint.|


### _burn

*Burn `amount` of `id` from `account`.
The `account` must not be the zero address.
The event should be emitted by the contract that inherits this contract.*


```solidity
function _burn(address account, uint256 id, uint256 amount) internal;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`account`|`address`|The address of the owner.|
|`id`|`uint256`|The token id.|
|`amount`|`uint256`|The amount to burn.|


### _batchTransferFrom

*Batch transfers `amounts` of `ids` from `from` to `to`.
The `to` must not be the zero address and the `ids` and `amounts` must have the same length.*


```solidity
function _batchTransferFrom(address from, address to, uint256[] calldata ids, uint256[] calldata amounts)
    internal
    checkLength(ids.length, amounts.length)
    notAddressZeroOrThis(to);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`from`|`address`|The address of the owner.|
|`to`|`address`|The address of the recipient.|
|`ids`|`uint256[]`|The list of token ids.|
|`amounts`|`uint256[]`|The list of amounts to transfer for each token id in `ids`.|


### _approveForAll

Grants or revokes permission to `spender` to transfer the caller's tokens, according to `approved`


```solidity
function _approveForAll(address owner, address spender, bool approved) internal notAddressZeroOrThis(owner);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`owner`|`address`|The address of the owner|
|`spender`|`address`|The address of the spender|
|`approved`|`bool`|The boolean value to grant or revoke permission|


### _notAddressZeroOrThis

*Reverts if the address is the zero address or the contract itself.*


```solidity
function _notAddressZeroOrThis(address account) internal view;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`account`|`address`|The address to check.|


### _checkLength

*Reverts if the length of the arrays are not equal.*


```solidity
function _checkLength(uint256 lengthA, uint256 lengthB) internal pure;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`lengthA`|`uint256`|The length of the first array.|
|`lengthB`|`uint256`|The length of the second array.|


