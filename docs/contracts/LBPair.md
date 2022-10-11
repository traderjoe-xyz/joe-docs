---
sidebar_position: 2
sidebar_label: LBPair
---

## LBPair

The implementation of Liquidity Book Pair that also acts as the receipt token for liquidity positions

### constructor

```solidity
constructor(contract ILBFactory _factory) public
```

Set the factory address

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _factory | contract ILBFactory | The address of the factory |

### initialize

```solidity
function initialize(contract IERC20 _tokenX, contract IERC20 _tokenY, uint24 _activeId, uint16 _sampleLifetime, bytes32 _packedFeeParameters) external override onlyFactory
```

Initialize the parameters of the LBPair

_The different parameters needs to be validated very cautiously.
It is highly recommended to never call this function directly, use the factory
as it validates the different parameters_

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _tokenX | contract IERC20 | The address of the tokenX. Can't be address 0 |
| _tokenY | contract IERC20 | The address of the tokenY. Can't be address 0 |
| _activeId | uint24 | The active id of the pair |
| _sampleLifetime | uint16 | The lifetime of a sample. It's the min time between 2 oracle's sample |
| _packedFeeParameters | bytes32 | The fee parameters packed in a single 256 bits slot |

### getReservesAndId

```solidity
function getReservesAndId() external view override returns (uint256 reserveX, uint256 reserveY, uint256 activeId)
```

View function to get the reserves and active id

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| reserveX | uint256 | The reserve of asset X |
| reserveY | uint256 | The reserve of asset Y |
| activeId | uint256 | The active id of the pair |

### getGlobalFees

```solidity
function getGlobalFees() external view override returns (uint256 feesXTotal, uint256 feesYTotal, uint256 feesXProtocol, uint256 feesYProtocol)
```

View function to get the global fees information, the total fees and those for protocol

_The fees for users are `total - protocol`_

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| feesXTotal | uint256 | The total fees of asset X |
| feesYTotal | uint256 | The total fees of asset Y |
| feesXProtocol | uint256 | The protocol fees of asset X |
| feesYProtocol | uint256 | The protocol fees of asset Y |

### getOracleParameters

```solidity
function getOracleParameters() external view override returns (uint256 oracleSampleLifetime, uint256 oracleSize, uint256 oracleActiveSize, uint256 oracleLastTimestamp, uint256 oracleId, uint256 min, uint256 max)
```

View function to get the oracle parameters

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| oracleSampleLifetime | uint256 | The lifetime of a sample, it accumulates information for up to this timestamp |
| oracleSize | uint256 | The size of the oracle (last ids can be empty) |
| oracleActiveSize | uint256 | The active size of the oracle (no empty data) |
| oracleLastTimestamp | uint256 | The timestamp of the creation of the oracle's latest sample |
| oracleId | uint256 | The index of the oracle's latest sample |
| min | uint256 | The min delta time of two samples |
| max | uint256 | The safe max delta time of two samples |

### getOracleSampleFrom

```solidity
function getOracleSampleFrom(uint256 _timeDelta) external view override returns (uint256 cumulativeId, uint256 cumulativeVolatilityAccumulated, uint256 cumulativeBinCrossed)
```

View function to get the oracle's sample at `_timeDelta` seconds

_Return a linearized sample, the weighted average of 2 neighboring samples_

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _timeDelta | uint256 | The number of seconds before the current timestamp |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| cumulativeId | uint256 | The weighted average cumulative id |
| cumulativeVolatilityAccumulated | uint256 | The weighted average cumulative volatility accumulated |
| cumulativeBinCrossed | uint256 | The weighted average cumulative bin crossed |

### feeParameters

```solidity
function feeParameters() external view override returns (struct FeeHelper.FeeParameters)
```

View function to get the fee parameters

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| [0] | struct FeeHelper.FeeParameters | The fee parameters |

### findFirstNonEmptyBinId

```solidity
function findFirstNonEmptyBinId(uint24 _id, bool _swapForY) external view override returns (uint24)
```

View function to get the first bin that isn't empty, will not be `_id` itself

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _id | uint24 | The bin id |
| _swapForY | bool | Whether you've swapping token X for token Y (true) or token Y for token X (false) |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| [0] | uint24 | The id of the non empty bin |

### getBin

```solidity
function getBin(uint24 _id) external view override returns (uint256 reserveX, uint256 reserveY)
```

View function to get the bin at `id`

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _id | uint24 | The bin id |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| reserveX | uint256 | The reserve of tokenX of the bin |
| reserveY | uint256 | The reserve of tokenY of the bin |

### pendingFees

```solidity
function pendingFees(address _account, uint256[] _ids) external view override returns (uint256 amountX, uint256 amountY)
```

View function to get the pending fees of a user

_The array must be strictly increasing to ensure uniqueness_

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _account | address | The address of the user |
| _ids | uint256[] | The list of ids |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| amountX | uint256 | The amount of tokenX pending |
| amountY | uint256 | The amount of tokenY pending |

### swap

```solidity
function swap(bool _swapForY, address _to) external override nonReentrant returns (uint256 amountXOut, uint256 amountYOut)
```

Performs a low level swap, this needs to be called from a contract which performs important safety checks

_Will swap the full amount that this contract received of token X or Y_

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _swapForY | bool | whether the token sent was Y (true) or X (false) |
| _to | address | The address of the recipient |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| amountXOut | uint256 | The amount of token X sent to `_to` |
| amountYOut | uint256 | The amount of token Y sent to `_to` |

### flashLoan

```solidity
function flashLoan(address _to, uint256 _amountXOut, uint256 _amountYOut, bytes _data) external override nonReentrant
```

Performs a flash loan

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _to | address | the address that will execute the external call |
| _amountXOut | uint256 | The amount of tokenX |
| _amountYOut | uint256 | The amount of tokenY |
| _data | bytes | The bytes data that will be forwarded to _to |

### mint

```solidity
function mint(uint256[] _ids, uint256[] _distributionX, uint256[] _distributionY, address _to) external override nonReentrant returns (uint256, uint256, uint256[] liquidityMinted)
```

Performs a low level add, this needs to be called from a contract which performs important safety checks.

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _ids | uint256[] | The list of ids to add liquidity |
| _distributionX | uint256[] | The distribution of tokenX with sum(_distributionX) = 1e18 (100%) or 0 (0%) |
| _distributionY | uint256[] | The distribution of tokenY with sum(_distributionY) = 1e18 (100%) or 0 (0%) |
| _to | address | The address of the recipient |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| [0] | uint256 | The amount of token X that was added to the pair |
| [1] | uint256 | The amount of token Y that was added to the pair |
| liquidityMinted | uint256[] | Amount of LBToken minted |

### burn

```solidity
function burn(uint256[] _ids, uint256[] _amounts, address _to) external override nonReentrant returns (uint256 amountX, uint256 amountY)
```

Performs a low level remove, this needs to be called from a contract which performs important safety checks

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _ids | uint256[] | The ids the user want to remove its liquidity |
| _amounts | uint256[] | The amount of token to burn |
| _to | address | The address of the recipient |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| amountX | uint256 | The amount of token X sent to `_to` |
| amountY | uint256 | The amount of token Y sent to `_to` |

### increaseOracleLength

```solidity
function increaseOracleLength(uint16 _newSize) external override
```

Increase the length of the oracle

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _newSize | uint16 | The new size of the oracle. Needs to be bigger than current one |

### collectFees

```solidity
function collectFees(address _account, uint256[] _ids) external override nonReentrant returns (uint256 amountX, uint256 amountY)
```

Collect fees of an user

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _account | address | The address of the user |
| _ids | uint256[] | The list of bin ids to collect fees in |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| amountX | uint256 | The amount of tokenX claimed |
| amountY | uint256 | The amount of tokenY claimed |

### collectProtocolFees

```solidity
function collectProtocolFees() external override nonReentrant returns (uint256 amountX, uint256 amountY)
```

Collect the protocol fees and send them to the feeRecipient

_The balances are not zeroed to save gas by not resetting the storage slot
Only callable by the fee recipient_

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| amountX | uint256 | The amount of tokenX claimed |
| amountY | uint256 | The amount of tokenY claimed |

### setFeesParameters

```solidity
function setFeesParameters(bytes32 _packedFeeParameters) external override onlyFactory 
```

Set the fees parameters

_Needs to be called by the factory that will validate the values
The bin step will not change
Only callable by the factory_

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _packedFeeParameters | bytes32 | The packed fee parameters |

### forceDecay

```solidity
function forceDecay() external override onlyFactory 
```

### _beforeTokenTransfer

```solidity
function _beforeTokenTransfer(address _from, address _to, uint256 _id, uint256 _amount) internal orverride(LBToken)
```

Collect and update fees before any token transfer, mint or burn

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _from | address | The address of the owner of the token |
| _to | address | The address of the recipient of the  token |
| _id | uint256 | The id of the token |
| _amount | uint256 | The amount of token of type `id` |


### _setFeesParameters

```solidity
function _setFeesParameters(bytes32 _packedFeeParameters) internal
```

Internal function to set the fee parameters of the pair

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _packedFeeParameters | bytes32 | The packed fee parameters |

### _getReservesAndId

```solidity
function _getReservesAndId() internal view returns (uint256 reserveX, uint256 reserveY, uint256 activeId)
```

Internal view function to get the reserves and active id

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| reserveX | uint256 | The reserve of asset X |
| reserveY | uint256 | The reserve of asset Y |
| activeId | uint256 | The active id of the pair |

### _getBin

```solidity
function _getBin(uint24 _id) internal view returns (uint256 reserveX, uint256 reserveY)
```

Internal view function to get the bin at `id`

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _id | uint24 | The bin id |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| reserveX | uint256 | The reserve of tokenX of the bin |
| reserveY | uint256 | The reserve of tokenY of the bin |

### _getGlobalFees

```solidity
function _getGlobalFees() internal view returns (uint256 feesXTotal, uint256 feesYTotal, uint256 feesXProtocol, uint256 feesYProtocol)
```

Internal view function to get the global fees information, the total fees and those for protocol

_The fees for users are `total - protocol`_

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| feesXTotal | uint256 | The total fees of asset X |
| feesYTotal | uint256 | The total fees of asset Y |
| feesXProtocol | uint256 | The protocol fees of asset X |
| feesYProtocol | uint256 | The protocol fees of asset Y |

### _getFlashLoanFee

```solidity
function _getFlashLoanFee(uint256 _amount, uint256 _fee) internal pure returns (uint256)
```

Internal pure function to return the flashloan fee amount

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _amount | uint256 | The amount to flashloan |
| _fee | uint256 | the fee percentage, in basis point |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| [0] | uint256 | The fee amount |

