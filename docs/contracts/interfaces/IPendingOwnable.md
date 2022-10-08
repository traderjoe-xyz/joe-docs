---
sidebar_position: 5
sidebar_label: IPendingOwnable
---

### PendingOwnerSet

```solidity
event PendingOwnerSet(address pendingOwner)
```

### OwnershipTransferred

```solidity
event OwnershipTransferred(address previousOwner, address newOwner)
```

### owner

```solidity
function owner() external view returns (address)
```

### pendingOwner

```solidity
function pendingOwner() external view returns (address)
```

### setPendingOwner

```solidity
function setPendingOwner(address pendingOwner) external
```

### revokePendingOwner

```solidity
function revokePendingOwner() external
```

### becomeOwner

```solidity
function becomeOwner() external
```

### renounceOwnership

```solidity
function renounceOwnership() external
```

