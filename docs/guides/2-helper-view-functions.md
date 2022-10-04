---
sidebar_position: 2
sidebar_label: Helper View Functions
---


# Helper view functions

## Swaps

### getSwapOut/getSwapIn

Below functions from `LBRouter` contract help calculate `amountIn`/`amountOut` for a swap including one pair.

```js
function getSwapIn(
    ILBPair LBPair,     // The address of the LBPair
    uint256 amountOut,  // The amount of token to receive
    bool swapForY       // Whether you swap X for Y (true), or Y for X (false)
) external view returns (
    uint256 amountIn,   // The amount of token to send in order to receive amountOut token
    uint256 feesIn      // Fees that are paid during this swap
    );

function getSwapOut(
    ILBPair LBPair,     // The address of the LBPair
    uint256 amountIn,   // The amount of token sent
    bool swapForY       // Whether you swap X for Y (true), or Y for X (false)
) external view returns (
    uint256 amountOut,  // The amount of token received if amountIn tokenX are sent
    uint256 feesIn      // Fees that are paid during this swap
    );
```

### findBestPathAmountIn / findBestPathAmountOut

Below functions from `LBQuoter` contract help calculate `amountIn`/`amountOut` for a swap including any number of pairs. 

```js
function findBestPathAmountOut(
    address[] memory _route, // List of the tokens to go through
    uint256 _amountOut       // Swap amount out
) public view returns (Quote memory quote)

function findBestPathAmountIn(
    address[] memory _route, // List of the tokens to go through
    uint256 _amountIn        // Swap amount in
) public view returns (Quote memory quote)

struct Quote {
    address[] route;
    address[] pairs;
    uint256[] binSteps;
    uint256[] amounts;
    uint256[] virtualAmountsWithoutSlippage;
}
```


## Liquidity add and removal

Below functions from `LBPair` contract help calculate parameters needed to add and remove liquidity.

### Get reserves and active bin ID

```js
function getReservesAndId()
    external
    view
    returns (
        uint256 reserveX,   // The reserve of asset X
        uint256 reserveY,   // The reserve of asset Y
        uint256 activeId    // The active id of the pair
    );
```

### Get bin information

```js
function getBin(
    uint24 id  // The bin id
    )  
    external view 
    returns (
        uint256 reserveX,   // The reserve of tokenX of the bin
        uint256 reserveY    // The reserve of tokenY of the bin
    );
```

### Get pending fees for user

```js
function pendingFees(
    address account,        // The address of the user 
    uint256[] memory ids    // The list of bin ids
    )
    external
    view
    returns (
        uint256 amountX,    // The amount of tokenX pending
        uint256 amountY     // The amount of tokenY pending
    );
```

## LB Token

Below functions from `LBToken` contract help calculate parameters needed to add and remove liquidity.

### Get number of bins deposited by user
```js
function userPositionNumber(
    address account     // The address of the account
    ) external view returns (uint256); // The number of non-zero balances of `account`
```

### Get balance of token in single bin owned by user
```js
function balanceOf(
    address account,    // The address of the owner
    uint256 id          // The token id
    ) external view returns (uint256); // The amount of tokens of type `id` owned by `_account`
```

### Get balance of token in many bins owned by users
```js
function balanceOfBatch(
    address[] memory accounts,  // The addresses of the owners
    uint256[] memory ids        // The token ids
    )
    external
    view
    returns (uint256[] memory batchBalances); // The balance for each (account, id) pair
```

### Get total token supply in bin
```js
function totalSupply(
    uint256 id  // The token id
    ) external view returns (uint256); // The total supply of that token id
```

