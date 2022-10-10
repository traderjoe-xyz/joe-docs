---
sidebar_position: 0
sidebar_label: 
---

## LBQuoter

Helper contract to determine best path through multiple markets

### Quote

```solidity
struct Quote {
  address[] route;
  address[] pairs;
  uint256[] binSteps;
  uint256[] amounts;
  uint256[] virtualAmountsWithoutSlippage;
  uint256[] fees;
}
```

### constructor

```solidity
constructor(address _routerV2, address _factoryV1, address _factoryV2) public
```

Constructor

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _routerV2 | address | Dex V2 router address |
| _factoryV1 | address | Dex V1 factory address |
| _factoryV2 | address | Dex V2 factory address |

### findBestPathFromAmountIn

```solidity
function findBestPathFromAmountIn(address[] _route, uint256 _amountIn) public view returns (struct LBQuoter.Quote quote)
```

Finds the best path given a list of tokens and the input amount wanted from the swap

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _route | address[] | List of the tokens to go through |
| _amountIn | uint256 | Swap amount in |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| quote | struct LBQuoter.Quote | The Quote structure containing the necessary element to perform the swap |

### findBestPathFromAmountOut

```solidity
function findBestPathFromAmountOut(address[] _route, uint256 _amountOut) public view returns (struct LBQuoter.Quote quote)
```

Finds the best path given a list of tokens and the output amount wanted from the swap

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _route | address[] | List of the tokens to go through |
| _amountOut | uint256 | Swap amount out |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| quote | struct LBQuoter.Quote | The Quote structure containing the necessary element to perform the swap |

### _getReserves

```solidity
function _getReserves(address _pair, address _tokenA, address _tokenB) internal view returns (uint256 reserveA, uint256 reserveB)
```

_Forked from JoeLibrary
Doesn't rely on the init code hash of the factory_

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _pair | address | Address of the pair |
| _tokenA | address | Address of token A |
| _tokenB | address | Address of token B |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| reserveA | uint256 | Reserve of token A in the pair |
| reserveB | uint256 | Reserve of token B in the pair |

### _getV2Quote

```solidity
function _getV2Quote(uint256 _amount, uint256 _activeId, uint256 _binStep, bool _swapForY) internal pure returns (uint256 quote)
```

_Calculates a quote for a V2 pair_

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _amount | uint256 | Amount in to consider |
| _activeId | uint256 | Current active Id of the considred pair |
| _binStep | uint256 | Bin step of the considered pair |
| _swapForY | bool | Boolean describing if we are swapping from X to Y or the opposite |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| quote | uint256 | Amount Out if _amount was swapped with no slippage and no fees |

