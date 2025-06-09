# LBQuoter
[Git Source](https://github.com/lfj-gg/joe-v2/blob/16f011d25e6bf6d0a0c479974345b623d491104f/src/LBQuoter.sol)

**Author:**
Trader Joe

Helper contract to determine best path through multiple markets
This contract shouldn't be used on-chain as it consumes a lot of gas
It should be used for off-chain purposes, like calculating the best path for a swap


## State Variables
### _factoryV1

```solidity
address private immutable _factoryV1;
```


### _legacyFactoryV2

```solidity
address private immutable _legacyFactoryV2;
```


### _factoryV2_1

```solidity
address private immutable _factoryV2_1;
```


### _factoryV2_2

```solidity
address private immutable _factoryV2_2;
```


### _legacyRouterV2

```solidity
address private immutable _legacyRouterV2;
```


### _routerV2_1

```solidity
address private immutable _routerV2_1;
```


### _routerV2_2

```solidity
address private immutable _routerV2_2;
```


## Functions
### constructor

Constructor


```solidity
constructor(
    address factoryV1,
    address legacyFactoryV2,
    address factoryV2_1,
    address factoryV2_2,
    address legacyRouterV2,
    address routerV2_1,
    address routerV2_2
);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`factoryV1`|`address`|Dex V1 factory address|
|`legacyFactoryV2`|`address`|Dex V2 factory address|
|`factoryV2_1`|`address`|Dex V2.1 factory address|
|`factoryV2_2`|`address`|Dex V2.2 factory address|
|`legacyRouterV2`|`address`|Dex V2 router address|
|`routerV2_1`|`address`|Dex V2.1 router address|
|`routerV2_2`|`address`|Dex V2.2 router address|


### getFactoryV1

Returns the Dex V1 factory address


```solidity
function getFactoryV1() public view returns (address factoryV1);
```
**Returns**

|Name|Type|Description|
|----|----|-----------|
|`factoryV1`|`address`|Dex V1 factory address|


### getLegacyFactoryV2

Returns the Dex V2 factory address


```solidity
function getLegacyFactoryV2() public view returns (address legacyFactoryV2);
```
**Returns**

|Name|Type|Description|
|----|----|-----------|
|`legacyFactoryV2`|`address`|Dex V2 factory address|


### getFactoryV2_1

Returns the Dex V2.1 factory address


```solidity
function getFactoryV2_1() public view returns (address factoryV2_1);
```
**Returns**

|Name|Type|Description|
|----|----|-----------|
|`factoryV2_1`|`address`|Dex V2.1 factory address|


### getFactoryV2_2

Returns the Dex V2.2 factory address


```solidity
function getFactoryV2_2() public view returns (address factoryV2_2);
```
**Returns**

|Name|Type|Description|
|----|----|-----------|
|`factoryV2_2`|`address`|Dex V2.2 factory address|


### getLegacyRouterV2

Returns the Dex V2 router address


```solidity
function getLegacyRouterV2() public view returns (address legacyRouterV2);
```
**Returns**

|Name|Type|Description|
|----|----|-----------|
|`legacyRouterV2`|`address`|Dex V2 router address|


### getRouterV2_1

Returns the Dex V2.1 router address


```solidity
function getRouterV2_1() public view returns (address routerV2_1);
```
**Returns**

|Name|Type|Description|
|----|----|-----------|
|`routerV2_1`|`address`|Dex V2.1 router address|


### getRouterV2_2

Returns the Dex V2.2 router address


```solidity
function getRouterV2_2() public view returns (address routerV2_2);
```
**Returns**

|Name|Type|Description|
|----|----|-----------|
|`routerV2_2`|`address`|Dex V2.2 router address|


### findBestPathFromAmountIn

Finds the best path given a list of tokens and the input amount wanted from the swap


```solidity
function findBestPathFromAmountIn(address[] calldata route, uint128 amountIn)
    public
    view
    returns (Quote memory quote);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`route`|`address[]`|List of the tokens to go through|
|`amountIn`|`uint128`|Swap amount in|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`quote`|`Quote`|The Quote structure containing the necessary element to perform the swap|


### findBestPathFromAmountOut

Finds the best path given a list of tokens and the output amount wanted from the swap


```solidity
function findBestPathFromAmountOut(address[] calldata route, uint128 amountOut)
    public
    view
    returns (Quote memory quote);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`route`|`address[]`|List of the tokens to go through|
|`amountOut`|`uint128`|Swap amount out|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`quote`|`Quote`|The Quote structure containing the necessary element to perform the swap|


### _getReserves

*Forked from JoeLibrary*

*Doesn't rely on the init code hash of the factory*


```solidity
function _getReserves(address pair, address tokenA, address tokenB)
    internal
    view
    returns (uint256 reserveA, uint256 reserveB);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`pair`|`address`|Address of the pair|
|`tokenA`|`address`|Address of token A|
|`tokenB`|`address`|Address of token B|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`reserveA`|`uint256`|Reserve of token A in the pair|
|`reserveB`|`uint256`|Reserve of token B in the pair|


### _getV2Quote

*Calculates a quote for a V2 pair*


```solidity
function _getV2Quote(uint256 amount, uint24 activeId, uint256 binStep, bool swapForY)
    internal
    pure
    returns (uint128 quote);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`amount`|`uint256`|Amount in to consider|
|`activeId`|`uint24`|Current active Id of the considred pair|
|`binStep`|`uint256`|Bin step of the considered pair|
|`swapForY`|`bool`|Boolean describing if we are swapping from X to Y or the opposite|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`quote`|`uint128`|Amount Out if _amount was swapped with no slippage and no fees|


## Errors
### LBQuoter_InvalidLength

```solidity
error LBQuoter_InvalidLength();
```

## Structs
### Quote
*The quote struct returned by the quoter
- route: address array of the token to go through
- pairs: address array of the pairs to go through
- binSteps: The bin step to use for each pair
- versions: The version to use for each pair
- amounts: The amounts of every step of the swap
- virtualAmountsWithoutSlippage: The virtual amounts of every step of the swap without slippage
- fees: The fees to pay for every step of the swap*


```solidity
struct Quote {
    address[] route;
    address[] pairs;
    uint256[] binSteps;
    ILBRouter.Version[] versions;
    uint128[] amounts;
    uint128[] virtualAmountsWithoutSlippage;
    uint128[] fees;
}
```

