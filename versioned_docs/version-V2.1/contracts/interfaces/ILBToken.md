## ILBToken

Required interface of LBToken contract

### TransferBatch

```solidity
event TransferBatch(
    address indexed sender, 
    address indexed from, 
    address indexed to, 
    uint256[] ids, 
    uint256[] amounts
    )
```

### ApprovalForAll

```solidity
event ApprovalForAll(
    address indexed account, 
    address indexed sender, 
    bool approved
    )
```

### name

```solidity
function name() public view virtual override returns (string memory)
```

### symbol

```solidity
function symbol() public view virtual override returns (string memory)
```


### totalSupply

```solidity
function totalSupply(uint256 id) public view virtual override returns (uint256)
```

### balanceOf

```solidity
function balanceOf(address account, uint256 id) public view virtual override returns (uint256)
```

### balanceOfBatch

```solidity
function balanceOfBatch(address[] memory accounts, uint256[] memory ids) public view virtual override checkLength(accounts.length, ids.length) returns (uint256[] memory batchBalances)
```

### isApprovedForAll

```solidity
function isApprovedForAll(address owner, address spender) public view virtual override returns (bool)
```

### approveForAll

```solidity
function approveForAll(address spender, bool approved) public virtual override
```

### batchTransferFrom

```solidity
function batchTransferFrom(address from, address to, uint256[] memory ids, uint256[] memory amounts) public virtual override checkApproval(from, msg.sender)
```
