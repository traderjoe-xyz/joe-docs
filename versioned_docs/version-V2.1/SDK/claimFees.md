---
sidebar_position: 4
sidebar_label: Claiming Fees
---

# Claiming Fees

This guide shows how to claim the rewards from your V2 liquidity pool using the SDKs, Subgraph, and Ethers.js. 

## 1. Required imports and constants for this guide

### Imports
```js
import { LBPairABI } from '@traderjoe-xyz/sdk-v2'
import { Wallet } from 'ethers'
import { BigNumber } from '@ethersproject/bignumber'
import { Contract } from '@ethersproject/contracts'
import { JsonRpcProvider } from '@ethersproject/providers'
```

### Constants: chain and wallet
```js
const AVAX_URL = 'https://api.avax.network/ext/bc/C/rpc'
const CHAIN_ID = ChainId.AVALANCHE
const PROVIDER = new JsonRpcProvider(AVAX_URL)
const WALLET_PK = "{WALLET_PRIVATE_KEY}"
const SIGNER = new Wallet(WALLET_PK, PROVIDER)
const ACCOUNT = await SIGNER.getAddress()
```

Note that in your project, you most likely will not hardcode the private key at any time. You would be using libraries like [web3react](https://github.com/Uniswap/web3-react) or [wagmi](https://wagmi.sh/) to connect to a wallet, sign messages, interact with contracts, and get the values for `PROVIDER`, `SIGNER` and `ACCOUNT`

### Initiaze LBPair contract using Ethers.js

```js
// init LBPair contract
const lbPairContract = new Contract(
  lbPairAddr,
  LBPairABI,
  SIGNER
)
```

Please refer [here](/versioned_docs/version-V2.1/guides/add-remove-liquidity.md#lbpair-and-active-bin) for instructions on how to get the `lbPairAddr` of a LBPair.

## 2. Get `userBinIds` from subgraph

Use the [subgraph](/versioned_docs/version-V2.1/subgraphs.md#avalanche) to fetch the binIds that the user holds or has ever held some liquidity. Below is an example of a GraphQL query to the subgraph's `LiquidityPositions` entity.

```graphql

{
  liquidityPositions(
    where: {
      user: "{ACCOUNT.toLowerCase()}"       # all lower case
      lbPair: "{lbPairAddr.toLowerCase()}"  # all lower case
    }
  ){
    id  	
    binsCount
    userBinLiquidities{
      liquidity
      binId
    }
  }
}
```
Assuming the above subgraph query has been made, `userBinIds` can now be derived:

```js
interface UserBinPosition {
  binId: string
  liquidity: string
}

let userBinLiquidities: UserBinPosition[]

// array of binIds where user has had liquidity
const userBinIds: number[] = userBinLiquidities.map(bl => Number(bl.binId))
```

## 3. Fetch pending fees

```js
const fees: {
  amountX: BigNumber
  amountY: BigNumber
} = await lbPairContract.pendingFees(ACCOUNT, userBinIds)
```

## 4 Collect fees

```js
const gasEstimate = await lbPairContract.estimateGas.collectFees(ACCOUNT, userBinIds)
await lbPairContract.collectFees(ACCOUNT, userBinIds, {
  gasLimit: calculateGasMargin(gasEstimate)
})
