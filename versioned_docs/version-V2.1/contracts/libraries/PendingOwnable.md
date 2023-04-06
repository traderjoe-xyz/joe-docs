## PendingOwnable

Contract module which provides a basic access control mechanism, where there is an account (an owner) that can be granted exclusive access to specific functions. The ownership of this contract is transferred using the push and pull pattern, the current owner set a `pendingOwner` using {setPendingOwner} and that address can then call {becomeOwner} to become the owner of that contract. The main logic and comments comes from OpenZeppelin's Ownable contract.

By default, the owner account will be the one that deploys the contract. This can later be changed with {setPendingOwner} and {becomeOwner}.

This module is used through inheritance. It will make available the modifier `onlyOwner`, which can be applied to your functions to restrict their use to the owner

#### `owner`

```solidity
function owner() public view returns (address)
```

Returns the address of the current owner

##### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
|   | address | The address of the current owner |

#### `pendingOwner`

```solidity
function pendingOwner() public view returns (address)
```

Returns the address of the current pending owner

##### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
|   | address | The address of the current pending owner |

#### `setPendingOwner`

```solidity
function setPendingOwner(address pendingOwner_) public onlyOwner
```

Sets the pending owner address. This address will be able to become the owner of this contract by calling {becomeOwner}

##### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| pendingOwner_ | address | The pending owner address |

#### `revokePendingOwner`

```solidity
function revokePendingOwner() public onlyOwner
```

Revoke the pending owner address. This address will not be able to call {becomeOwner} to become the owner anymore. Can only be called by the owner

#### `becomeOwner`

```solidity
function becomeOwner() public onlyPendingOwner
```

Transfers the ownership to the new owner (`pendingOwner). Can only be called by the pending owner

#### `renounceOwnership`

```solidity
function renounceOwnership() public onlyOwner
```

Leaves the contract without owner. It will not be possible to call `onlyOwner` functions anymore. Can only be called by the current owner.


