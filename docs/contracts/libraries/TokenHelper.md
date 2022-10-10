---
sidebar_position: 0
sidebar_label: TokenHelper
---

## TokenHelper

Wrappers around ERC20 operations that throw on failure (when the token
contract returns false). Tokens that return no value (and instead revert or
throw on failure) are also supported, non-reverting calls are assumed to be
successful.
To use this library you can add a `using TokenHelper for IERC20;` statement to your contract,
which allows you to call the safe operation as `token.safeTransfer(...)`

### safeTransferFrom

```solidity
function safeTransferFrom(contract IERC20 token, address owner, address recipient, uint256 amount) internal
```

Transfers token only if the amount is greater than zero

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| token | contract IERC20 | The address of the token |
| owner | address | The owner of the tokens |
| recipient | address | The address of the recipient |
| amount | uint256 | The amount to send |

### safeTransfer

```solidity
function safeTransfer(contract IERC20 token, address recipient, uint256 amount) internal
```

Transfers token only if the amount is greater than zero

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| token | contract IERC20 | The address of the token |
| recipient | address | The address of the recipient |
| amount | uint256 | The amount to send |

### received

```solidity
function received(contract IERC20 token, uint256 reserve, uint256 fees) internal view returns (uint256)
```

Returns the amount of token received by the pair

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| token | contract IERC20 | The address of the token |
| reserve | uint256 | The total reserve of token |
| fees | uint256 | The total fees of token |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| [0] | uint256 | The amount received by the pair |

