# TokenHelper
[Git Source](https://github.com/traderjoe-xyz/joe-v2/blob/16f011d25e6bf6d0a0c479974345b623d491104f/src/libraries/TokenHelper.sol)

**Author:**
Trader Joe

Wrappers around ERC20 operations that throw on failure (when the token
contract returns false). Tokens that return no value (and instead revert or
throw on failure) are also supported, non-reverting calls are assumed to be
successful.
To use this library you can add a `using TokenHelper for IERC20;` statement to your contract,
which allows you to call the safe operation as `token.safeTransfer(...)`


## Functions
### safeTransferFrom

Transfers token and reverts if the transfer fails


```solidity
function safeTransferFrom(IERC20 token, address owner, address recipient, uint256 amount) internal;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`token`|`IERC20`|The address of the token|
|`owner`|`address`|The owner of the tokens|
|`recipient`|`address`|The address of the recipient|
|`amount`|`uint256`|The amount to send|


### safeTransfer

Transfers token and reverts if the transfer fails


```solidity
function safeTransfer(IERC20 token, address recipient, uint256 amount) internal;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`token`|`IERC20`|The address of the token|
|`recipient`|`address`|The address of the recipient|
|`amount`|`uint256`|The amount to send|


### _callAndCatch


```solidity
function _callAndCatch(IERC20 token, bytes memory data) internal;
```

## Errors
### TokenHelper__TransferFailed

```solidity
error TokenHelper__TransferFailed();
```

