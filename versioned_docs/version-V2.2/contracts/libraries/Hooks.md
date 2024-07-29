# Hooks
[Git Source](https://github.com/traderjoe-xyz/joe-v2/blob/16f011d25e6bf6d0a0c479974345b623d491104f/src/libraries/Hooks.sol)

This library contains functions that should be used to interact with hooks


## State Variables
### BEFORE_SWAP_FLAG

```solidity
bytes32 internal constant BEFORE_SWAP_FLAG = bytes32(uint256(1 << 160));
```


### AFTER_SWAP_FLAG

```solidity
bytes32 internal constant AFTER_SWAP_FLAG = bytes32(uint256(1 << 161));
```


### BEFORE_FLASH_LOAN_FLAG

```solidity
bytes32 internal constant BEFORE_FLASH_LOAN_FLAG = bytes32(uint256(1 << 162));
```


### AFTER_FLASH_LOAN_FLAG

```solidity
bytes32 internal constant AFTER_FLASH_LOAN_FLAG = bytes32(uint256(1 << 163));
```


### BEFORE_MINT_FLAG

```solidity
bytes32 internal constant BEFORE_MINT_FLAG = bytes32(uint256(1 << 164));
```


### AFTER_MINT_FLAG

```solidity
bytes32 internal constant AFTER_MINT_FLAG = bytes32(uint256(1 << 165));
```


### BEFORE_BURN_FLAG

```solidity
bytes32 internal constant BEFORE_BURN_FLAG = bytes32(uint256(1 << 166));
```


### AFTER_BURN_FLAG

```solidity
bytes32 internal constant AFTER_BURN_FLAG = bytes32(uint256(1 << 167));
```


### BEFORE_TRANSFER_FLAG

```solidity
bytes32 internal constant BEFORE_TRANSFER_FLAG = bytes32(uint256(1 << 168));
```


### AFTER_TRANSFER_FLAG

```solidity
bytes32 internal constant AFTER_TRANSFER_FLAG = bytes32(uint256(1 << 169));
```


## Functions
### encode

*Helper function to encode the hooks parameters to a single bytes32 value*


```solidity
function encode(Parameters memory parameters) internal pure returns (bytes32 hooksParameters);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`parameters`|`Parameters`|The hooks parameters|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`hooksParameters`|`bytes32`|The encoded hooks parameters|


### decode

*Helper function to decode the hooks parameters from a single bytes32 value*


```solidity
function decode(bytes32 hooksParameters) internal pure returns (Parameters memory parameters);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`hooksParameters`|`bytes32`|The encoded hooks parameters|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`parameters`|`Parameters`|The hooks parameters|


### getHooks

*Helper function to get the hooks address from the encoded hooks parameters*


```solidity
function getHooks(bytes32 hooksParameters) internal pure returns (address hooks);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`hooksParameters`|`bytes32`|The encoded hooks parameters|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`hooks`|`address`|The hooks address|


### setHooks

*Helper function to set the hooks address in the encoded hooks parameters*


```solidity
function setHooks(bytes32 hooksParameters, address newHooks) internal pure returns (bytes32);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`hooksParameters`|`bytes32`|The encoded hooks parameters|
|`newHooks`|`address`|The new hooks address|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bytes32`|hooksParameters The updated hooks parameters|


### getFlags

*Helper function to get the flags from the encoded hooks parameters*


```solidity
function getFlags(bytes32 hooksParameters) internal pure returns (bytes12 flags);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`hooksParameters`|`bytes32`|The encoded hooks parameters|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`flags`|`bytes12`|The flags|


### onHooksSet

*Helper function call the onHooksSet function on the hooks contract, only if the
hooksParameters is not 0*


```solidity
function onHooksSet(bytes32 hooksParameters, bytes calldata onHooksSetData) internal;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`hooksParameters`|`bytes32`|The encoded hooks parameters|
|`onHooksSetData`|`bytes`|The data to pass to the onHooksSet function|


### beforeSwap

*Helper function to call the beforeSwap function on the hooks contract, only if the
BEFORE_SWAP_FLAG is set in the hooksParameters*


```solidity
function beforeSwap(bytes32 hooksParameters, address sender, address to, bool swapForY, bytes32 amountsIn) internal;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`hooksParameters`|`bytes32`|The encoded hooks parameters|
|`sender`|`address`|The sender|
|`to`|`address`|The recipient|
|`swapForY`|`bool`|Whether the swap is for Y|
|`amountsIn`|`bytes32`|The amounts in|


### afterSwap

*Helper function to call the afterSwap function on the hooks contract, only if the
AFTER_SWAP_FLAG is set in the hooksParameters*


```solidity
function afterSwap(bytes32 hooksParameters, address sender, address to, bool swapForY, bytes32 amountsOut) internal;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`hooksParameters`|`bytes32`|The encoded hooks parameters|
|`sender`|`address`|The sender|
|`to`|`address`|The recipient|
|`swapForY`|`bool`|Whether the swap is for Y|
|`amountsOut`|`bytes32`|The amounts out|


### beforeFlashLoan

*Helper function to call the beforeFlashLoan function on the hooks contract, only if the
BEFORE_FLASH_LOAN_FLAG is set in the hooksParameters*


```solidity
function beforeFlashLoan(bytes32 hooksParameters, address sender, address to, bytes32 amounts) internal;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`hooksParameters`|`bytes32`|The encoded hooks parameters|
|`sender`|`address`|The sender|
|`to`|`address`|The recipient|
|`amounts`|`bytes32`|The amounts|


### afterFlashLoan

*Helper function to call the afterFlashLoan function on the hooks contract, only if the
AFTER_FLASH_LOAN_FLAG is set in the hooksParameters*


```solidity
function afterFlashLoan(bytes32 hooksParameters, address sender, address to, bytes32 fees, bytes32 feesReceived)
    internal;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`hooksParameters`|`bytes32`|The encoded hooks parameters|
|`sender`|`address`|The sender|
|`to`|`address`|The recipient|
|`fees`|`bytes32`|The fees|
|`feesReceived`|`bytes32`|The fees received|


### beforeMint

*Helper function to call the beforeMint function on the hooks contract, only if the
BEFORE_MINT_FLAG is set in the hooksParameters*


```solidity
function beforeMint(
    bytes32 hooksParameters,
    address sender,
    address to,
    bytes32[] calldata liquidityConfigs,
    bytes32 amountsReceived
) internal;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`hooksParameters`|`bytes32`|The encoded hooks parameters|
|`sender`|`address`|The sender|
|`to`|`address`|The recipient|
|`liquidityConfigs`|`bytes32[]`|The liquidity configs|
|`amountsReceived`|`bytes32`|The amounts received|


### afterMint

*Helper function to call the afterMint function on the hooks contract, only if the
AFTER_MINT_FLAG is set in the hooksParameters*


```solidity
function afterMint(
    bytes32 hooksParameters,
    address sender,
    address to,
    bytes32[] calldata liquidityConfigs,
    bytes32 amountsIn
) internal;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`hooksParameters`|`bytes32`|The encoded hooks parameters|
|`sender`|`address`|The sender|
|`to`|`address`|The recipient|
|`liquidityConfigs`|`bytes32[]`|The liquidity configs|
|`amountsIn`|`bytes32`|The amounts in|


### beforeBurn

*Helper function to call the beforeBurn function on the hooks contract, only if the
BEFORE_BURN_FLAG is set in the hooksParameters*


```solidity
function beforeBurn(
    bytes32 hooksParameters,
    address sender,
    address from,
    address to,
    uint256[] calldata ids,
    uint256[] calldata amountsToBurn
) internal;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`hooksParameters`|`bytes32`|The encoded hooks parameters|
|`sender`|`address`|The sender|
|`from`|`address`|The sender|
|`to`|`address`|The recipient|
|`ids`|`uint256[]`|The ids|
|`amountsToBurn`|`uint256[]`|The amounts to burn|


### afterBurn

*Helper function to call the afterBurn function on the hooks contract, only if the
AFTER_BURN_FLAG is set in the hooksParameters*


```solidity
function afterBurn(
    bytes32 hooksParameters,
    address sender,
    address from,
    address to,
    uint256[] calldata ids,
    uint256[] calldata amountsToBurn
) internal;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`hooksParameters`|`bytes32`|The encoded hooks parameters|
|`sender`|`address`|The sender|
|`from`|`address`|The sender|
|`to`|`address`|The recipient|
|`ids`|`uint256[]`|The ids|
|`amountsToBurn`|`uint256[]`|The amounts to burn|


### beforeBatchTransferFrom

*Helper function to call the beforeTransferFrom function on the hooks contract, only if the
BEFORE_TRANSFER_FLAG is set in the hooksParameters*


```solidity
function beforeBatchTransferFrom(
    bytes32 hooksParameters,
    address sender,
    address from,
    address to,
    uint256[] calldata ids,
    uint256[] calldata amounts
) internal;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`hooksParameters`|`bytes32`|The encoded hooks parameters|
|`sender`|`address`|The sender|
|`from`|`address`|The sender|
|`to`|`address`|The recipient|
|`ids`|`uint256[]`|The list of ids|
|`amounts`|`uint256[]`|The list of amounts|


### afterBatchTransferFrom

*Helper function to call the afterTransferFrom function on the hooks contract, only if the
AFTER_TRANSFER_FLAG is set in the hooksParameters*


```solidity
function afterBatchTransferFrom(
    bytes32 hooksParameters,
    address sender,
    address from,
    address to,
    uint256[] calldata ids,
    uint256[] calldata amounts
) internal;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`hooksParameters`|`bytes32`|The encoded hooks parameters|
|`sender`|`address`|The sender|
|`from`|`address`|The sender|
|`to`|`address`|The recipient|
|`ids`|`uint256[]`|The list of ids|
|`amounts`|`uint256[]`|The list of amounts|


### _safeCall

*Helper function to call the hooks contract and verify the call was successful
by matching the expected selector with the returned data*


```solidity
function _safeCall(bytes32 hooksParameters, bytes memory data) private;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`hooksParameters`|`bytes32`|The encoded hooks parameters|
|`data`|`bytes`|The data to pass to the hooks contract|


## Errors
### Hooks__CallFailed

```solidity
error Hooks__CallFailed();
```

## Structs
### Parameters

```solidity
struct Parameters {
    address hooks;
    bool beforeSwap;
    bool afterSwap;
    bool beforeFlashLoan;
    bool afterFlashLoan;
    bool beforeMint;
    bool afterMint;
    bool beforeBurn;
    bool afterBurn;
    bool beforeBatchTransferFrom;
    bool afterBatchTransferFrom;
}
```

