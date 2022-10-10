---
sidebar_position: 0
sidebar_label: 
---

## ILBToken

Required interface of LBToken contract

### TransferSingle

```solidity
event TransferSingle(address sender, address from, address to, uint256 id, uint256 amount)
```

### TransferBatch

```solidity
event TransferBatch(address sender, address from, address to, uint256[] ids, uint256[] amounts)
```

### ApprovalForAll

```solidity
event ApprovalForAll(address account, address sender, bool approved)
```

### name

```solidity
function name() external view returns (string)
```

### symbol

```solidity
function symbol() external view returns (string)
```

### balanceOf

```solidity
function balanceOf(address account, uint256 id) external view returns (uint256)
```

### balanceOfBatch

```solidity
function balanceOfBatch(address[] accounts, uint256[] ids) external view returns (uint256[] batchBalances)
```

### userPositionAtIndex

```solidity
function userPositionAtIndex(address account, uint256 index) external view returns (uint256)
```

### userPositionNumber

```solidity
function userPositionNumber(address account) external view returns (uint256)
```

### totalSupply

```solidity
function totalSupply(uint256 id) external view returns (uint256)
```

### isApprovedForAll

```solidity
function isApprovedForAll(address owner, address spender) external view returns (bool)
```

### setApprovalForAll

```solidity
function setApprovalForAll(address sender, bool approved) external
```

### safeTransferFrom

```solidity
function safeTransferFrom(address from, address to, uint256 id, uint256 amount) external
```

### safeBatchTransferFrom

```solidity
function safeBatchTransferFrom(address from, address to, uint256[] id, uint256[] amount) external
```

