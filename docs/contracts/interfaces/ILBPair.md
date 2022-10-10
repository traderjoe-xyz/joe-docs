---
sidebar_position: 0
sidebar_label: ILBPair
---

## ILBPair

Required interface of LBPair contract

### Bin

```solidity
struct Bin {
  uint112 reserveX;
  uint112 reserveY;
  uint256 accTokenXPerShare;
  uint256 accTokenYPerShare;
}
```

### PairInformation

```solidity
struct PairInformation {
  uint24 activeId;
  uint136 reserveX;
  uint136 reserveY;
  uint16 oracleSampleLifetime;
  uint16 oracleSize;
  uint16 oracleActiveSize;
  uint40 oracleLastTimestamp;
  uint16 oracleId;
  struct FeeHelper.FeesDistribution feesX;
  struct FeeHelper.FeesDistribution feesY;
}
```

### Debts

```solidity
struct Debts {
  uint256 debtX;
  uint256 debtY;
}
```

### Fees

```solidity
struct Fees {
  uint128 tokenX;
  uint128 tokenY;
}
```

### MintInfo

```solidity
struct MintInfo {
  uint256 amountXIn;
  uint256 amountYIn;
  uint256 amountXAddedToPair;
  uint256 amountYAddedToPair;
  uint256 activeFeeX;
  uint256 activeFeeY;
  uint256 totalDistributionX;
  uint256 totalDistributionY;
  uint256 id;
  uint256 amountX;
  uint256 amountY;
  uint256 distributionX;
  uint256 distributionY;
}
```

### Swap

```solidity
event Swap(address sender, address recipient, uint24 id, uint256 amountXIn, uint256 amountYIn, uint256 amountXOut, uint256 amountYOut, uint256 volatilityAccumulated, uint256 feesX, uint256 feesY)
```

### FlashLoan

```solidity
event FlashLoan(address sender, address recipient, uint256 amountX, uint256 amountY, uint256 feesX, uint256 feesY)
```

### LiquidityAdded

```solidity
event LiquidityAdded(address sender, address recipient, uint256 id, uint256 minted, uint256 amountX, uint256 amountY, uint256 distributionX, uint256 distributionY)
```

### CompositionFee

```solidity
event CompositionFee(address sender, address recipient, uint256 id, uint256 feesX, uint256 feesY)
```

### LiquidityRemoved

```solidity
event LiquidityRemoved(address sender, address recipient, uint256 id, uint256 burned, uint256 amountX, uint256 amountY)
```

### FeesCollected

```solidity
event FeesCollected(address sender, address recipient, uint256 amountX, uint256 amountY)
```

### ProtocolFeesCollected

```solidity
event ProtocolFeesCollected(address sender, address recipient, uint256 amountX, uint256 amountY)
```

### OracleSizeIncreased

```solidity
event OracleSizeIncreased(uint256 previousSize, uint256 newSize)
```

### tokenX

```solidity
function tokenX() external view returns (contract IERC20)
```

### tokenY

```solidity
function tokenY() external view returns (contract IERC20)
```

### factory

```solidity
function factory() external view returns (contract ILBFactory)
```

### getReservesAndId

```solidity
function getReservesAndId() external view returns (uint256 reserveX, uint256 reserveY, uint256 activeId)
```

### getGlobalFees

```solidity
function getGlobalFees() external view returns (uint256 feesXTotal, uint256 feesYTotal, uint256 feesXProtocol, uint256 feesYProtocol)
```

### getOracleParameters

```solidity
function getOracleParameters() external view returns (uint256 oracleSampleLifetime, uint256 oracleSize, uint256 oracleActiveSize, uint256 oracleLastTimestamp, uint256 oracleId, uint256 min, uint256 max)
```

### getOracleSampleFrom

```solidity
function getOracleSampleFrom(uint256 timeDelta) external view returns (uint256 cumulativeId, uint256 cumulativeAccumulator, uint256 cumulativeBinCrossed)
```

### feeParameters

```solidity
function feeParameters() external view returns (struct FeeHelper.FeeParameters)
```

### findFirstNonEmptyBinId

```solidity
function findFirstNonEmptyBinId(uint24 id_, bool sentTokenY) external view returns (uint24 id)
```

### getBin

```solidity
function getBin(uint24 id) external view returns (uint256 reserveX, uint256 reserveY)
```

### pendingFees

```solidity
function pendingFees(address account, uint256[] ids) external view returns (uint256 amountX, uint256 amountY)
```

### swap

```solidity
function swap(bool sentTokenY, address to) external returns (uint256 amountXOut, uint256 amountYOut)
```

### flashLoan

```solidity
function flashLoan(address to, uint256 amountXOut, uint256 amountYOut, bytes data) external
```

### mint

```solidity
function mint(uint256[] ids, uint256[] distributionX, uint256[] distributionY, address to) external returns (uint256 amountXAddedToPair, uint256 amountYAddedToPair, uint256[] liquidityMinted)
```

### burn

```solidity
function burn(uint256[] ids, uint256[] amounts, address to) external returns (uint256 amountX, uint256 amountY)
```

### increaseOracleLength

```solidity
function increaseOracleLength(uint16 newSize) external
```

### collectFees

```solidity
function collectFees(address account, uint256[] ids) external returns (uint256 amountX, uint256 amountY)
```

### collectProtocolFees

```solidity
function collectProtocolFees() external returns (uint256 amountX, uint256 amountY)
```

### setFeesParameters

```solidity
function setFeesParameters(bytes32 packedFeeParameters) external
```

### forceDecay

```solidity
function forceDecay() external
```

### initialize

```solidity
function initialize(contract IERC20 tokenX, contract IERC20 tokenY, uint24 activeId, uint16 sampleLifetime, bytes32 packedFeeParameters) external
```

