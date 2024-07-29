# ImmutableClone
[Git Source](https://github.com/traderjoe-xyz/joe-v2/blob/16f011d25e6bf6d0a0c479974345b623d491104f/src/libraries/ImmutableClone.sol)

**Authors:**
Trader Joe, Solady (https://github.com/vectorized/solady/blob/main/src/utils/LibClone.sol), Minimal proxy by 0age (https://github.com/0age), Clones with immutable args by wighawag, zefram.eth, Saw-mon & Natalie
(https://github.com/Saw-mon-and-Natalie/clones-with-immutable-args)

Minimal immutable proxy library.

*Minimal proxy:
Although the sw0nt pattern saves 5 gas over the erc-1167 pattern during runtime,
it is not supported out-of-the-box on Etherscan. Hence, we choose to use the 0age pattern,
which saves 4 gas over the erc-1167 pattern during runtime, and has the smallest bytecode.*

*Clones with immutable args (CWIA):
The implementation of CWIA here doesn't implements a `receive()` as it is not needed for LB.*


## Functions
### cloneDeterministic

*Deploys a deterministic clone of `implementation` using immutable arguments encoded in `data`, with `salt`*


```solidity
function cloneDeterministic(address implementation, bytes memory data, bytes32 salt)
    internal
    returns (address instance);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`implementation`|`address`|The address of the implementation|
|`data`|`bytes`|The encoded immutable arguments|
|`salt`|`bytes32`|The salt|


### initCodeHash

---------------------------------------------------------------------------------------------------+
CREATION (10 bytes)                                                                                |
---------------------------------------------------------------------------------------------------|
Opcode     | Mnemonic          | Stack     | Memory                                                |
---------------------------------------------------------------------------------------------------|
61 runSize | PUSH2 runSize     | r         |                                                       |
3d         | RETURNDATASIZE    | 0 r       |                                                       |
81         | DUP2              | r 0 r     |                                                       |
60 offset  | PUSH1 offset      | o r 0 r   |                                                       |
3d         | RETURNDATASIZE    | 0 o r 0 r |                                                       |
39         | CODECOPY          | 0 r       | [0..runSize): runtime code                            |
f3         | RETURN            |           | [0..runSize): runtime code                            |
---------------------------------------------------------------------------------------------------|
RUNTIME (98 bytes + extraLength)                                                                   |
---------------------------------------------------------------------------------------------------|
Opcode   | Mnemonic       | Stack                    | Memory                                      |
---------------------------------------------------------------------------------------------------|
|
::: copy calldata to memory :::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::: |
36       | CALLDATASIZE   | cds                      |                                             |
3d       | RETURNDATASIZE | 0 cds                    |                                             |
3d       | RETURNDATASIZE | 0 0 cds                  |                                             |
37       | CALLDATACOPY   |                          | [0..cds): calldata                          |
|
::: keep some values in stack :::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::: |
3d       | RETURNDATASIZE | 0                        | [0..cds): calldata                          |
3d       | RETURNDATASIZE | 0 0                      | [0..cds): calldata                          |
3d       | RETURNDATASIZE | 0 0 0                    | [0..cds): calldata                          |
3d       | RETURNDATASIZE | 0 0 0 0                  | [0..cds): calldata                          |
61 extra | PUSH2 extra    | e 0 0 0 0                | [0..cds): calldata                          |
|
::: copy extra data to memory :::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::: |
80       | DUP1           | e e 0 0 0 0              | [0..cds): calldata                          |
60 0x35  | PUSH1 0x35     | 0x35 e e 0 0 0 0         | [0..cds): calldata                          |
36       | CALLDATASIZE   | cds 0x35 e e 0 0 0 0     | [0..cds): calldata                          |
39       | CODECOPY       | e 0 0 0 0                | [0..cds): calldata, [cds..cds+e): extraData |
|
::: delegate call to the implementation contract ::::::::::::::::::::::::::::::::::::::::::::::::: |
36       | CALLDATASIZE   | cds e 0 0 0 0            | [0..cds): calldata, [cds..cds+e): extraData |
01       | ADD            | cds+e 0 0 0 0            | [0..cds): calldata, [cds..cds+e): extraData |
3d       | RETURNDATASIZE | 0 cds+e 0 0 0 0          | [0..cds): calldata, [cds..cds+e): extraData |
73 addr  | PUSH20 addr    | addr 0 cds+e 0 0 0 0     | [0..cds): calldata, [cds..cds+e): extraData |
5a       | GAS            | gas addr 0 cds+e 0 0 0 0 | [0..cds): calldata, [cds..cds+e): extraData |
f4       | DELEGATECALL   | success 0 0              | [0..cds): calldata, [cds..cds+e): extraData |
|
::: copy return data to memory ::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::: |
3d       | RETURNDATASIZE | rds success 0 0          | [0..cds): calldata, [cds..cds+e): extraData |
3d       | RETURNDATASIZE | rds rds success 0 0      | [0..cds): calldata, [cds..cds+e): extraData |
93       | SWAP4          | 0 rds success 0 rds      | [0..cds): calldata, [cds..cds+e): extraData |
80       | DUP1           | 0 0 rds success 0 rds    | [0..cds): calldata, [cds..cds+e): extraData |
3e       | RETURNDATACOPY | success 0 rds            | [0..rds): returndata                        |
|
60 0x33  | PUSH1 0x33     | 0x33 success 0 rds       | [0..rds): returndata                        |
57       | JUMPI          | 0 rds                    | [0..rds): returndata                        |
|
::: revert ::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::: |
fd       | REVERT         |                          | [0..rds): returndata                        |
|
::: return ::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::: |
5b       | JUMPDEST       | 0 rds                    | [0..rds): returndata                        |
f3       | RETURN         |                          | [0..rds): returndata                        |
---------------------------------------------------------------------------------------------------+

*Returns the initialization code hash of the clone of `implementation`
using immutable arguments encoded in `data`.
Used for mining vanity addresses with create2crunch.*


```solidity
function initCodeHash(address implementation, bytes memory data) internal pure returns (bytes32 hash);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`implementation`|`address`|The address of the implementation contract.|
|`data`|`bytes`|The encoded immutable arguments.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`hash`|`bytes32`|The initialization code hash.|


### predictDeterministicAddress

*Returns the address of the deterministic clone of
`implementation` using immutable arguments encoded in `data`, with `salt`, by `deployer`.*


```solidity
function predictDeterministicAddress(address implementation, bytes memory data, bytes32 salt, address deployer)
    internal
    pure
    returns (address predicted);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`implementation`|`address`|The address of the implementation.|
|`data`|`bytes`|The immutable arguments of the implementation.|
|`salt`|`bytes32`|The salt used to compute the address.|
|`deployer`|`address`|The address of the deployer.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`predicted`|`address`|The predicted address.|


### predictDeterministicAddress

*Returns the address when a contract with initialization code hash,
`hash`, is deployed with `salt`, by `deployer`.*


```solidity
function predictDeterministicAddress(bytes32 hash, bytes32 salt, address deployer)
    internal
    pure
    returns (address predicted);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`hash`|`bytes32`|The initialization code hash.|
|`salt`|`bytes32`|The salt used to compute the address.|
|`deployer`|`address`|The address of the deployer.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`predicted`|`address`|The predicted address.|


## Errors
### DeploymentFailed

```solidity
error DeploymentFailed();
```

### PackedDataTooBig

```solidity
error PackedDataTooBig();
```

