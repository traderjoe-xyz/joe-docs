---
sidebar_label: SwapHelper
---

### getAmounts

```solidity
function getAmounts(struct ILBPair.Bin bin, struct FeeHelper.FeeParameters fp, uint256 activeId, bool swapForY, uint256 amountIn) internal pure returns (uint256 amountInToBin, uint256 amountOutOfBin, struct FeeHelper.FeesDistribution fees)
```

Returns the swap amounts in the current bin

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| bin | struct ILBPair.Bin | The bin information |
| fp | struct FeeHelper.FeeParameters | The fee parameters |
| activeId | uint256 | The active id of the pair |
| swapForY | bool | Whether you've swapping token X for token Y (true) or token Y for token X (false) |
| amountIn | uint256 | The amount sent by the user |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| amountInToBin | uint256 | The amount of token that is added to the bin without the fees |
| amountOutOfBin | uint256 | The amount of token that is removed from the bin |
| fees | struct FeeHelper.FeesDistribution | The swap fees |

### updateFees

```solidity
function updateFees(struct ILBPair.Bin bin, struct FeeHelper.FeesDistribution pairFees, struct FeeHelper.FeesDistribution fees, bool swapForY, uint256 totalSupply) internal pure
```

Update the fees of the pair and accumulated token per share of the bin

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| bin | struct ILBPair.Bin | The bin information |
| pairFees | struct FeeHelper.FeesDistribution | The current fees of the pair information |
| fees | struct FeeHelper.FeesDistribution | The fees amounts added to the pairFees |
| swapForY | bool | whether the token sent was Y (true) or X (false) |
| totalSupply | uint256 | The total supply of the token id |

### updateReserves

```solidity
function updateReserves(struct ILBPair.Bin bin, struct ILBPair.PairInformation pair, bool swapForY, uint112 amountInToBin, uint112 amountOutOfBin) internal pure
```

Update reserves

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| bin | struct ILBPair.Bin | The bin information |
| pair | struct ILBPair.PairInformation | The pair information |
| swapForY | bool | whether the token sent was Y (true) or X (false) |
| amountInToBin | uint112 | The amount of token that is added to the bin without fees |
| amountOutOfBin | uint112 | The amount of token that is removed from the bin |

