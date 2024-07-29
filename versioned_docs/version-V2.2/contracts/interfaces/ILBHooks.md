# ILBHooks
[Git Source](https://github.com/traderjoe-xyz/joe-v2/blob/16f011d25e6bf6d0a0c479974345b623d491104f/src/interfaces/ILBHooks.sol)


## Functions
### getLBPair


```solidity
function getLBPair() external view returns (ILBPair);
```

### isLinked


```solidity
function isLinked() external view returns (bool);
```

### onHooksSet


```solidity
function onHooksSet(bytes32 hooksParameters, bytes calldata onHooksSetData) external returns (bytes4);
```

### beforeSwap


```solidity
function beforeSwap(address sender, address to, bool swapForY, bytes32 amountsIn) external returns (bytes4);
```

### afterSwap


```solidity
function afterSwap(address sender, address to, bool swapForY, bytes32 amountsOut) external returns (bytes4);
```

### beforeFlashLoan


```solidity
function beforeFlashLoan(address sender, address to, bytes32 amounts) external returns (bytes4);
```

### afterFlashLoan


```solidity
function afterFlashLoan(address sender, address to, bytes32 fees, bytes32 feesReceived) external returns (bytes4);
```

### beforeMint


```solidity
function beforeMint(address sender, address to, bytes32[] calldata liquidityConfigs, bytes32 amountsReceived)
    external
    returns (bytes4);
```

### afterMint


```solidity
function afterMint(address sender, address to, bytes32[] calldata liquidityConfigs, bytes32 amountsIn)
    external
    returns (bytes4);
```

### beforeBurn


```solidity
function beforeBurn(address sender, address from, address to, uint256[] calldata ids, uint256[] calldata amountsToBurn)
    external
    returns (bytes4);
```

### afterBurn


```solidity
function afterBurn(address sender, address from, address to, uint256[] calldata ids, uint256[] calldata amountsToBurn)
    external
    returns (bytes4);
```

### beforeBatchTransferFrom


```solidity
function beforeBatchTransferFrom(
    address sender,
    address from,
    address to,
    uint256[] calldata ids,
    uint256[] calldata amounts
) external returns (bytes4);
```

### afterBatchTransferFrom


```solidity
function afterBatchTransferFrom(
    address sender,
    address from,
    address to,
    uint256[] calldata ids,
    uint256[] calldata amounts
) external returns (bytes4);
```

