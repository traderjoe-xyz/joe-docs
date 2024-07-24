# LBBaseHooks
[Git Source](https://github.com/traderjoe-xyz/joe-v2/blob/16f011d25e6bf6d0a0c479974345b623d491104f/src/LBBaseHooks.sol)

**Inherits:**
[ILBHooks](/src/interfaces/ILBHooks.md)

Base contract for LBPair hooks
This contract is meant to be inherited by any contract that wants to implement LBPair hooks


## Functions
### onlyTrustedCaller

*Modifier to check that the caller is the trusted caller*


```solidity
modifier onlyTrustedCaller();
```

### getLBPair

*Returns the LBPair contract*


```solidity
function getLBPair() external view override returns (ILBPair);
```
**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`ILBPair`|The LBPair contract|


### isLinked

*Returns whether the contract is linked to the pair or not*


```solidity
function isLinked() external view override returns (bool);
```
**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bool`|Whether the contract is linked to the pair or not|


### onHooksSet

Hook called by the pair when the hooks parameters are set

*Only callable by the pair*


```solidity
function onHooksSet(bytes32 hooksParameters, bytes calldata onHooksSetData)
    external
    override
    onlyTrustedCaller
    returns (bytes4);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`hooksParameters`|`bytes32`|The hooks parameters|
|`onHooksSetData`|`bytes`|The onHooksSet data|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bytes4`|The function selector|


### beforeSwap

Hook called by the pair before a swap

*Only callable by the pair*


```solidity
function beforeSwap(address sender, address to, bool swapForY, bytes32 amountsIn)
    external
    override
    onlyTrustedCaller
    returns (bytes4);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`sender`|`address`|The address that initiated the swap|
|`to`|`address`|The address that will receive the swapped tokens|
|`swapForY`|`bool`|Whether the swap is for token Y|
|`amountsIn`|`bytes32`|The amounts in|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bytes4`|The function selector|


### afterSwap

Hook called by the pair after a swap

*Only callable by the pair*


```solidity
function afterSwap(address sender, address to, bool swapForY, bytes32 amountsOut)
    external
    override
    onlyTrustedCaller
    returns (bytes4);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`sender`|`address`|The address that initiated the swap|
|`to`|`address`|The address that received the swapped tokens|
|`swapForY`|`bool`|Whether the swap was for token Y|
|`amountsOut`|`bytes32`|The amounts out|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bytes4`|The function selector|


### beforeFlashLoan

Hook called by the pair before a flash loan

*Only callable by the pair*


```solidity
function beforeFlashLoan(address sender, address to, bytes32 amounts)
    external
    override
    onlyTrustedCaller
    returns (bytes4);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`sender`|`address`|The address that initiated the flash loan|
|`to`|`address`|The address that will receive the flash loaned tokens|
|`amounts`|`bytes32`|The amounts|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bytes4`|The function selector|


### afterFlashLoan

Hook called by the pair after a flash loan

*Only callable by the pair*


```solidity
function afterFlashLoan(address sender, address to, bytes32 fees, bytes32 feesReceived)
    external
    override
    onlyTrustedCaller
    returns (bytes4);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`sender`|`address`|The address that initiated the flash loan|
|`to`|`address`|The address that received the flash loaned tokens|
|`fees`|`bytes32`|The flashloan fees|
|`feesReceived`|`bytes32`|The fees received|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bytes4`|The function selector|


### beforeMint

Hook called by the pair before minting

*Only callable by the pair*


```solidity
function beforeMint(address sender, address to, bytes32[] calldata liquidityConfigs, bytes32 amountsReceived)
    external
    override
    onlyTrustedCaller
    returns (bytes4);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`sender`|`address`|The address that initiated the mint|
|`to`|`address`|The address that will receive the minted tokens|
|`liquidityConfigs`|`bytes32[]`|The liquidity configurations|
|`amountsReceived`|`bytes32`|The amounts received|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bytes4`|The function selector|


### afterMint

Hook called by the pair after minting

*Only callable by the pair*


```solidity
function afterMint(address sender, address to, bytes32[] calldata liquidityConfigs, bytes32 amountsIn)
    external
    override
    onlyTrustedCaller
    returns (bytes4);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`sender`|`address`|The address that initiated the mint|
|`to`|`address`|The address that received the minted tokens|
|`liquidityConfigs`|`bytes32[]`|The liquidity configurations|
|`amountsIn`|`bytes32`|The amounts in|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bytes4`|The function selector|


### beforeBurn

Hook called by the pair before burning

*Only callable by the pair*


```solidity
function beforeBurn(address sender, address from, address to, uint256[] calldata ids, uint256[] calldata amountsToBurn)
    external
    override
    onlyTrustedCaller
    returns (bytes4);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`sender`|`address`|The address that initiated the burn|
|`from`|`address`|The address that will burn the tokens|
|`to`|`address`|The address that will receive the burned tokens|
|`ids`|`uint256[]`|The token ids|
|`amountsToBurn`|`uint256[]`|The amounts to burn|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bytes4`|The function selector|


### afterBurn

Hook called by the pair after burning

*Only callable by the pair*


```solidity
function afterBurn(address sender, address from, address to, uint256[] calldata ids, uint256[] calldata amountsToBurn)
    external
    override
    onlyTrustedCaller
    returns (bytes4);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`sender`|`address`|The address that initiated the burn|
|`from`|`address`|The address that burned the tokens|
|`to`|`address`|The address that received the burned tokens|
|`ids`|`uint256[]`|The token ids|
|`amountsToBurn`|`uint256[]`|The amounts to burn|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bytes4`|The function selector|


### beforeBatchTransferFrom

Hook called by the pair before a batch transfer

*Only callable by the pair*


```solidity
function beforeBatchTransferFrom(
    address sender,
    address from,
    address to,
    uint256[] calldata ids,
    uint256[] calldata amounts
) external override onlyTrustedCaller returns (bytes4);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`sender`|`address`|The address that initiated the transfer|
|`from`|`address`|The address that will transfer the tokens|
|`to`|`address`|The address that will receive the tokens|
|`ids`|`uint256[]`|The token ids|
|`amounts`|`uint256[]`|The amounts|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bytes4`|The function selector|


### afterBatchTransferFrom

Hook called by the pair after a batch transfer

*Only callable by the pair*


```solidity
function afterBatchTransferFrom(
    address sender,
    address from,
    address to,
    uint256[] calldata ids,
    uint256[] calldata amounts
) external override onlyTrustedCaller returns (bytes4);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`sender`|`address`|The address that initiated the transfer|
|`from`|`address`|The address that transferred the tokens|
|`to`|`address`|The address that received the tokens|
|`ids`|`uint256[]`|The token ids|
|`amounts`|`uint256[]`|The amounts|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bytes4`|The function selector|


### _checkTrustedCaller

*Checks that the caller is the trusted caller, otherwise reverts*


```solidity
function _checkTrustedCaller() internal view virtual;
```

### _isLinked

*Checks if the contract is linked to the pair*


```solidity
function _isLinked() internal view virtual returns (bool);
```
**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bool`|Whether the contract is linked to the pair or not|


### _getLBPair

*Returns the LBPair contract*


```solidity
function _getLBPair() internal view virtual returns (ILBPair);
```

### _onHooksSet

Internal function to be overridden that is called when the hooks parameters are set


```solidity
function _onHooksSet(bytes32 hooksParameters, bytes calldata onHooksSetData) internal virtual;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`hooksParameters`|`bytes32`|The hooks parameters|
|`onHooksSetData`|`bytes`|The onHooksSet data|


### _beforeSwap

Internal function to be overridden that is called before a swap


```solidity
function _beforeSwap(address sender, address to, bool swapForY, bytes32 amountsIn) internal virtual;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`sender`|`address`|The address that initiated the swap|
|`to`|`address`|The address that will receive the swapped tokens|
|`swapForY`|`bool`|Whether the swap is for token Y|
|`amountsIn`|`bytes32`|The amounts in|


### _afterSwap

Internal function to be overridden that is called after a swap


```solidity
function _afterSwap(address sender, address to, bool swapForY, bytes32 amountsOut) internal virtual;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`sender`|`address`|The address that initiated the swap|
|`to`|`address`|The address that received the swapped tokens|
|`swapForY`|`bool`|Whether the swap was for token Y|
|`amountsOut`|`bytes32`|The amounts out|


### _beforeFlashLoan

Internal function to be overridden that is called before a flash loan


```solidity
function _beforeFlashLoan(address sender, address to, bytes32 amounts) internal virtual;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`sender`|`address`|The address that initiated the flash loan|
|`to`|`address`|The address that will receive the flash loaned tokens|
|`amounts`|`bytes32`|The amounts|


### _afterFlashLoan

Internal function to be overridden that is called after a flash loan


```solidity
function _afterFlashLoan(address sender, address to, bytes32 fees, bytes32 feesReceived) internal virtual;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`sender`|`address`|The address that initiated the flash loan|
|`to`|`address`|The address that received the flash loaned tokens|
|`fees`|`bytes32`|The flashloan fees|
|`feesReceived`|`bytes32`|The fees received|


### _beforeMint

Internal function to be overridden that is called before minting


```solidity
function _beforeMint(address sender, address to, bytes32[] calldata liquidityConfigs, bytes32 amountsReceived)
    internal
    virtual;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`sender`|`address`|The address that initiated the mint|
|`to`|`address`|The address that will receive the minted tokens|
|`liquidityConfigs`|`bytes32[]`|The liquidity configurations|
|`amountsReceived`|`bytes32`|The amounts received|


### _afterMint

Internal function to be overridden that is called after minting


```solidity
function _afterMint(address sender, address to, bytes32[] calldata liquidityConfigs, bytes32 amountsIn)
    internal
    virtual;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`sender`|`address`|The address that initiated the mint|
|`to`|`address`|The address that received the minted tokens|
|`liquidityConfigs`|`bytes32[]`|The liquidity configurations|
|`amountsIn`|`bytes32`|The amounts in|


### _beforeBurn

Internal function to be overridden that is called before burning


```solidity
function _beforeBurn(address sender, address from, address to, uint256[] calldata ids, uint256[] calldata amountsToBurn)
    internal
    virtual;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`sender`|`address`|The address that initiated the burn|
|`from`|`address`|The address that will burn the tokens|
|`to`|`address`|The address that will receive the burned tokens|
|`ids`|`uint256[]`|The token ids|
|`amountsToBurn`|`uint256[]`|The amounts to burn|


### _afterBurn

Internal function to be overridden that is called after burning


```solidity
function _afterBurn(address sender, address from, address to, uint256[] calldata ids, uint256[] calldata amountsToBurn)
    internal
    virtual;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`sender`|`address`|The address that initiated the burn|
|`from`|`address`|The address that burned the tokens|
|`to`|`address`|The address that received the burned tokens|
|`ids`|`uint256[]`|The token ids|
|`amountsToBurn`|`uint256[]`|The amounts to burn|


### _beforeBatchTransferFrom

Internal function to be overridden that is called before a batch transfer


```solidity
function _beforeBatchTransferFrom(
    address sender,
    address from,
    address to,
    uint256[] calldata ids,
    uint256[] calldata amounts
) internal virtual;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`sender`|`address`|The address that initiated the transfer|
|`from`|`address`|The address that will transfer the tokens|
|`to`|`address`|The address that will receive the tokens|
|`ids`|`uint256[]`|The token ids|
|`amounts`|`uint256[]`|The amounts|


### _afterBatchTransferFrom

Internal function to be overridden that is called after a batch transfer


```solidity
function _afterBatchTransferFrom(
    address sender,
    address from,
    address to,
    uint256[] calldata ids,
    uint256[] calldata amounts
) internal virtual;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`sender`|`address`|The address that initiated the transfer|
|`from`|`address`|The address that transferred the tokens|
|`to`|`address`|The address that received the tokens|
|`ids`|`uint256[]`|The token ids|
|`amounts`|`uint256[]`|The amounts|


## Errors
### LBBaseHooks__InvalidCaller

```solidity
error LBBaseHooks__InvalidCaller(address caller);
```

### LBBaseHooks__NotLinked

```solidity
error LBBaseHooks__NotLinked();
```

