# Constants
[Git Source](https://github.com/lfj-gg/joe-v2/blob/16f011d25e6bf6d0a0c479974345b623d491104f/src/libraries/Constants.sol)

**Author:**
Trader Joe

Set of constants for Liquidity Book contracts


## State Variables
### SCALE_OFFSET

```solidity
uint8 internal constant SCALE_OFFSET = 128;
```


### SCALE

```solidity
uint256 internal constant SCALE = 1 << SCALE_OFFSET;
```


### PRECISION

```solidity
uint256 internal constant PRECISION = 1e18;
```


### SQUARED_PRECISION

```solidity
uint256 internal constant SQUARED_PRECISION = PRECISION * PRECISION;
```


### MAX_FEE

```solidity
uint256 internal constant MAX_FEE = 0.1e18;
```


### MAX_PROTOCOL_SHARE

```solidity
uint256 internal constant MAX_PROTOCOL_SHARE = 2_500;
```


### BASIS_POINT_MAX

```solidity
uint256 internal constant BASIS_POINT_MAX = 10_000;
```


### MAX_LIQUIDITY_PER_BIN

```solidity
uint256 internal constant MAX_LIQUIDITY_PER_BIN =
    65251743116719673010965625540244653191619923014385985379600384103134737;
```


### CALLBACK_SUCCESS
*The expected return after a successful flash loan*


```solidity
bytes32 internal constant CALLBACK_SUCCESS = keccak256("LBPair.onFlashLoan");
```


