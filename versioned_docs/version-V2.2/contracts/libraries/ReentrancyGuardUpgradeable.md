# ReentrancyGuardUpgradeable
[Git Source](https://github.com/lfj-gg/joe-v2/blob/16f011d25e6bf6d0a0c479974345b623d491104f/src/libraries/ReentrancyGuardUpgradeable.sol)

**Inherits:**
Initializable

*This contract is a fork of the `ReentrancyGuardUpgradeable` contract from OpenZeppelin
that has been modified to update the `_nonReentrantBefore` and `_nonReentrantAfter`
functions to `internal` visibility.
Contract module that helps prevent reentrant calls to a function.
Inheriting from `ReentrancyGuard` will make the `nonReentrant` modifier
available, which can be applied to functions to make sure there are no nested
(reentrant) calls to them.
Note that because there is a single `nonReentrant` guard, functions marked as
`nonReentrant` may not call one another. This can be worked around by making
those functions `private`, and then adding `external` `nonReentrant` entry
points to them.
TIP: If you would like to learn more about reentrancy and alternative ways
to protect against it, check out our blog post
https://blog.openzeppelin.com/reentrancy-after-istanbul/[Reentrancy After Istanbul].*


## State Variables
### NOT_ENTERED

```solidity
uint256 private constant NOT_ENTERED = 1;
```


### ENTERED

```solidity
uint256 private constant ENTERED = 2;
```


### ReentrancyGuardStorageLocation

```solidity
bytes32 private constant ReentrancyGuardStorageLocation =
    0x9b779b17422d0df92223018b32b4d1fa46e071723d6817e2486d003becc55f00;
```


## Functions
### _getReentrancyGuardStorage


```solidity
function _getReentrancyGuardStorage() private pure returns (ReentrancyGuardStorage storage $);
```

### __ReentrancyGuard_init


```solidity
function __ReentrancyGuard_init() internal onlyInitializing;
```

### __ReentrancyGuard_init_unchained


```solidity
function __ReentrancyGuard_init_unchained() internal onlyInitializing;
```

### nonReentrant

*Prevents a contract from calling itself, directly or indirectly.
Calling a `nonReentrant` function from another `nonReentrant`
function is not supported. It is possible to prevent this from happening
by making the `nonReentrant` function external, and making it call a
`private` function that does the actual work.*


```solidity
modifier nonReentrant();
```

### _nonReentrantBefore


```solidity
function _nonReentrantBefore() internal;
```

### _nonReentrantAfter


```solidity
function _nonReentrantAfter() internal;
```

### _reentrancyGuardEntered

*Returns true if the reentrancy guard is currently set to "entered", which indicates there is a
`nonReentrant` function in the call stack.*


```solidity
function _reentrancyGuardEntered() internal view returns (bool);
```

## Errors
### ReentrancyGuardReentrantCall
*Unauthorized reentrant call.*


```solidity
error ReentrancyGuardReentrantCall();
```

## Structs
### ReentrancyGuardStorage

```solidity
struct ReentrancyGuardStorage {
    uint256 _status;
}
```

