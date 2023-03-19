## ILBPair

Required interface of LBPair contract

### DepositedToBins

```solidity
event DepositedToBins(address indexed sender, address indexed to, uint256[] ids, bytes32[] amounts)
```

### WithdrawnFromBins

```solidity
event WithdrawnFromBins(address indexed sender, address indexed to, uint256[] ids, bytes32[] amounts)
```

### CompositionFees

```solidity
event CompositionFees(address indexed sender, uint24 id, bytes32 totalFees, bytes32 protocolFees)
```

### CollectedProtocolFees

```solidity
event CollectedProtocolFees(address indexed feeRecipient, bytes32 protocolFees)
```

### Swap

```solidity
event Swap(
    address indexed sender,
    address indexed to,
    uint24 id,
    bytes32 amountsIn,
    bytes32 amountsOut,
    uint24 volatilityAccumulator,
    bytes32 totalFees,
    bytes32 protocolFees
    )
```

### StaticFeeParametersSet

```solidity
event StaticFeeParametersSet(
    address indexed sender,
    uint16 baseFactor,
    uint16 filterPeriod,
    uint16 decayPeriod,
    uint16 reductionFactor,
    uint24 variableFeeControl,
    uint16 protocolShare,
    uint24 maxVolatilityAccumulator
    )
```

### FlashLoan

```solidity
event FlashLoan(
    address indexed sender,
    ILBFlashLoanCallback indexed receiver,
    uint24 activeId,
    bytes32 amounts,
    bytes32 totalFees,
    bytes32 protocolFees
    )
```

### OracleLengthIncreased

```solidity
event OracleLengthIncreased(address indexed sender, uint16 oracleLength)
```

### ForcedDecay

```solidity
event ForcedDecay(address indexed sender, uint24 idReference, uint24 volatilityReference)
```

### initialize

```solidity
function initialize(
    uint16 baseFactor,
    uint16 filterPeriod,
    uint16 decayPeriod,
    uint16 reductionFactor,
    uint24 variableFeeControl,
    uint16 protocolShare,
    uint24 maxVolatilityAccumulator,
    uint24 activeId
) external override onlyFactory
```


### getFactory

```solidity
function getFactory() external view override returns (ILBFactory factory)
```

### getTokenX

```solidity
function getTokenX() external pure override returns (IERC20 tokenX)
```

### getTokenY

```solidity
function getTokenY() external pure override returns (IERC20 tokenY)
```

### getBinStep

```solidity
function getBinStep() external pure override returns (uint16)
```

### getReserves

```solidity
function getReserves() external view override returns (uint128 reserveX, uint128 reserveY)
```

### getActiveId

```solidity
function getActiveId() external view override returns (uint24 activeId)
```

### getBin

```solidity
function getBin(uint24 id) external view override returns (uint128 binReserveX, uint128 binReserveY)
```

### getNextNonEmptyBin

```solidity
function getNextNonEmptyBin(bool swapForY, uint24 id) external view override returns (uint24 nextId)
```

### getProtocolFees

```solidity
function getProtocolFees() external view returns (uint128 protocolFeeX, uint128 protocolFeeY)
```

### getStaticFeeParameters

```solidity
function getStaticFeeParameters() external view returns (uint16 baseFactor, uint16 filterPeriod, uint16 decayPeriod, uint16 reductionFactor, uint24 variableFeeControl, uint16 protocolShare, uint24 maxVolatilityAccumulator)
```


### getVariableFeeParameters

```solidity
function getVariableFeeParameters() external view returns (uint24 volatilityAccumulator, uint24 volatilityReference, uint24 idReference, uint40 timeOfLastUpdate)
```


### getOracleParameters

```solidity
function getOracleParameters() external view returns (uint8 sampleLifetime, uint16 size, uint16 activeSize, uint40 lastUpdated, uint40 firstTimestamp)
```

### getOracleSampleAt

```solidity
function getOracleSampleAt(uint40 lookupTimestamp) external view returns (uint64 cumulativeId, uint64 cumulativeVolatility, uint64 cumulativeBinCrossed)
```


### getPriceFromId

```solidity
function getPriceFromId(uint24 id) external pure returns (uint256 price)
```

### getIdFromPrice

```solidity
function getIdFromPrice(uint256 price) external pure returns (uint24 id)
```


### getSwapIn

```solidity
function getSwapIn(uint128 amountOut, bool swapForY) external view returns (uint128 amountIn, uint128 amountOutLeft, uint128 fee)
```

### getSwapOut

```solidity
function getSwapOut(uint128 amountIn, bool swapForY) external view override returns (uint128 amountInLeft, uint128 amountOut, uint128 fee)
```

### swap

```solidity
function swap(bool swapForY, address to) external override nonReentrant returns (bytes32 amountsOut)
```

### flashLoan

```solidity
function flashLoan(ILBFlashLoanCallback receiver, bytes32 amounts, bytes calldata data) external override nonReentrant
```

### mint

```solidity
function mint(address to, bytes32[] calldata liquidityConfigs, address refundTo) external override nonReentrant returns (bytes32 amountsReceived, bytes32 amountsLeft, uint256[] memory liquidityMinted)
```

### burn

```solidity
function burn(address from, address to, uint256[] calldata ids, uint256[] calldata amountsToBurn) external override nonReentrant checkApproval(from, msg.sender) returns (bytes32[] memory amounts)
```


### collectProtocolFees

```solidity
function collectProtocolFees() external override nonReentrant onlyProtocolFeeRecipient returns (bytes32 collectedProtocolFees)
```


### increaseOracleLength

```solidity
function increaseOracleLength(uint16 newLength) external override
```

### setStaticFeeParameters

```solidity
function setStaticFeeParameters(
    uint16 baseFactor,
    uint16 filterPeriod,
    uint16 decayPeriod,
    uint16 reductionFactor,
    uint24 variableFeeControl,
    uint16 protocolShare,
    uint24 maxVolatilityAccumulator
) external override onlyFactory
```


### forceDecay

```solidity
function forceDecay() external override onlyFactory
```
