---
sidebar_position: 0
sidebar_label: PendingOwnable
---

## PendingOwnable

Contract module which provides a basic access control mechanism, where
there is an account (an owner) that can be granted exclusive access to
specific functions. The ownership of this contract is transferred using the
push and pull pattern, the current owner set a `pendingOwner` using
{setPendingOwner} and that address can then call {becomeOwner} to become the
owner of that contract. The main logic and comments comes from OpenZeppelin's
Ownable contract.

By default, the owner account will be the one that deploys the contract. This
can later be changed with {setPendingOwner} and {becomeOwner}.

This module is used through inheritance. It will make available the modifier
`onlyOwner`, which can be applied to your functions to restrict their use to
the owner

### constructor

```solidity
constructor() public
```

Initializes the contract setting the deployer as the initial owner

### owner

```solidity
function owner() public view returns (address)
```

Returns the address of the current owner

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| [0] | address | The address of the current owner |

### pendingOwner

```solidity
function pendingOwner() public view returns (address)
```

Returns the address of the current pending owner

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| [0] | address | The address of the current pending owner |

### setPendingOwner

```solidity
function setPendingOwner(address pendingOwner_) public
```

Sets the pending owner address. This address will be able to become
the owner of this contract by calling {becomeOwner}

### revokePendingOwner

```solidity
function revokePendingOwner() public
```

Revoke the pending owner address. This address will not be able to
call {becomeOwner} to become the owner anymore.
Can only be called by the owner

### becomeOwner

```solidity
function becomeOwner() public
```

Transfers the ownership to the new owner (`pendingOwner).
Can only be called by the pending owner

### renounceOwnership

```solidity
function renounceOwnership() public
```

Leaves the contract without owner. It will not be possible to call
`onlyOwner` functions anymore. Can only be called by the current owner.

NOTE: Renouncing ownership will leave the contract without an owner,
thereby removing any functionality that is only available to the owner.

### _transferOwnership

```solidity
function _transferOwnership(address _newOwner) internal virtual
```

Transfers ownership of the contract to a new account (`newOwner`).
Internal function without access restriction.

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _newOwner | address | The address of the new owner |

### _setPendingOwner

```solidity
function _setPendingOwner(address pendingOwner_) internal virtual
```

Push the new owner, it needs to be pulled to be effective.
Internal function without access restriction.

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| pendingOwner_ | address | The address of the new pending owner |

