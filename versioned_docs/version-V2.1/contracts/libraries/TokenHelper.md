## Token Helper 

Wrappers around ERC20 operations that throw on failure (when the token contract returns false). Tokens that return no value (and instead revert or throw on failure) are also supported, non-reverting calls are assumed to be successful.

To use this library you can add a `using TokenHelper for IERC20;` statement to your contract, which allows you to call the safe operation as `token.safeTransfer(...)`

### safeTransferFrom

```solidity
function safeTransferFrom(IERC20 token, address owner, address recipient, uint256 amount) internal
```

Transfers token and reverts if the transfer fails.

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| token | IERC20 | The address of the token |
| owner | address | The owner of the tokens |
| recipient | address | The address of the recipient |
| amount | uint256 | The amount to send |

### safeTransfer

```solidity
function safeTransfer(IERC20 token, address recipient, uint256 amount) internal
```

Transfers token and reverts if the transfer fails.

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| token | IERC20 | The address of the token |
| recipient | address | The address of the recipient |
| amount | uint256 | The amount to send |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| None | - | If the transfer fails, the function reverts |