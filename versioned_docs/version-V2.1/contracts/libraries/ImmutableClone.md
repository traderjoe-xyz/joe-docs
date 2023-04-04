## Immutable Clone

Minimal immutable proxy library.

### cloneDeterministic

```solidity
function cloneDeterministic(address implementation, bytes memory data, bytes32 salt) internal returns (address instance)
```

Deploys a deterministic clone of `implementation` using immutable arguments encoded in `data`, with `salt`

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| implementation | address | The address of the implementation |
| data | bytes | The encoded immutable arguments |
| salt | bytes32 | The salt |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| instance | address | Returns the address of the clone instance |

### initCodeHash

```solidity
function initCodeHash(address implementation, bytes memory data) internal pure returns (bytes32 hash)
```

Returns the initialization code hash of the clone of `implementation` using immutable arguments encoded in `data`. Used for mining vanity addresses with create2crunch.

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| implementation | address | The address of the implementation contract |
| data | bytes | The encoded immutable arguments |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| hash | bytes32 | Returns the initialization code hash |

### predictDeterministicAddress

```solidity
function predictDeterministicAddress(address implementation, bytes memory data, bytes32 salt, address deployer) internal pure returns (address predicted)
```

Returns the address of the deterministic clone of `implementation` using immutable arguments encoded in `data`, with `salt`, by `deployer`.

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| implementation | address | The address of the implementation |
| data | bytes | The immutable arguments of the implementation |
| salt | bytes32 | The salt used to compute the address |
| deployer | address | The address of the deployer |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| predicted | address | Returns the predicted address |

### predictDeterministicAddress

```solidity
function predictDeterministicAddress(bytes32 hash, bytes32 salt, address deployer) internal pure returns (address predicted)
```

Returns the address when a contract with initialization code hash, `hash`, is deployed with `salt`, by `deployer`.

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| hash | bytes32 | The initialization code hash |
| salt | bytes32 | The salt used to compute the address |
| deployer | address | The address of the deployer |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| predicted | address | Returns the predicted address |