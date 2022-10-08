---
sidebar_label: FeeDistributionHelper
---

### flashLoanHelper

```solidity
function flashLoanHelper(struct FeeHelper.FeesDistribution _fees, struct FeeHelper.FeesDistribution _pairFees, contract IERC20 _token, uint256 _reserve) internal
```

Checks that the flash loan was done accordingly and update fees

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _fees | struct FeeHelper.FeesDistribution | The fees received by the pair |
| _pairFees | struct FeeHelper.FeesDistribution | The fees of the pair |
| _token | contract IERC20 | The address of the token received |
| _reserve | uint256 | The stored reserve of the current bin |

### getTokenPerShare

```solidity
function getTokenPerShare(struct FeeHelper.FeesDistribution _fees, uint256 _totalSupply) internal pure returns (uint256)
```

Calculate the tokenPerShare when fees are added

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _fees | struct FeeHelper.FeesDistribution | The fees received by the pair |
| _totalSupply | uint256 | the total supply of a specific bin |

