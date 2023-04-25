---
sidebar_position: 3
sidebar_label: Removing Liquidity
---

# Removing Liquidity

This guide shows how to remove liquidity from a V2 pool using the SDKs, Subgraph, and Ethers.js. In this example, we will be removing liquidity from a LBPair of USDC/USDC.e/2bps

## 1. Required imports and constants for this guide

### Imports
```js
import { 
  LB_ROUTER_V21_ADDRESS,
  LBRouterV21ABI,
  LBPairV21ABI,
  LBPairABI,
  PairV2
} from '@traderjoe-xyz/sdk-v2'
import { Token, JSBI, Percent } from '@traderjoe-xyz/sdk'
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

### Constants: tokens and LBPair bin step
```js
const USDC = new Token(
  CHAIN_ID,
  '0xB97EF9Ef8734C71904D8002F8b6Bc66Dd9c48a6E',
  6,
  'USDC',
  'USD Coin'
)

const USDC_E = new Token(
  CHAIN_ID,
  '0xA7D7079b0FEaD91F3e65f86E8915Cb59c1a4C664',
  6,
  'USDC.e',
  'USD Coin bridged'
)

const BIN_STEP = "2"
```

## 2. Fetch all data neccesary to compute the pooled token amounts

The following data needs to be fetched to compute the user's USDC and USDC.e amounts currently deposited in the USDC/USDC.e/2bps pool. This is because the pooled token amounts will constantly change depending on the current active bin, and the bins' `reserveX`/`reserveY` and `totalSupply`. 

Please note that this step will be significantly simplified in the future with the support of the **LiquidityAmounts** periphery contract and our own DEX API.  

### LBPair and active bin

```js
const pair = new PairV2(USDC, USDC_E)
const binStep = Number(BIN_STEP)
const isV21 = true // set to true if it's a V2.1 pair.
const lbPair = await pair.fetchLBPair(binStep, isV21, PROVIDER, CHAIN_ID)
const lbPairAddr = lbPair.LBPair

const lbPairData = await PairV2.getLBPairReservesAndId(lbPair.LBPair, isV21, PROVIDER)
const activeBinId = lbPairData.activeId.toNumber()
```

### Liquidity positions 

Use the [subgraph](/versioned_docs/version-V2.1/subgraphs.md#avalanche) to fetch your positions (Only applicable to `V2` pairs). You need all the `binId`s where you have liquidity and the amount of `liquidity` in each bin. Below is an example of a GraphQL query to the subgraph's `LiquidityPositions` entity.
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
    userBinLiquidities( where: { liquidity_gt: 0 }){
      liquidity
      binId
    }
  }
}
```

We'll assume you have fetched your positions from the subgraph, resulting in `UserBinPosition[]`. We can then get the `userPositionIds`.

```js
interface UserBinPosition {
  binId: string
  liquidity: string
}

let userBinLiquidities: UserBinPosition[]

// array of binIds where user has liquidity
const userPositionIds: string[] = userBinLiquidities.map(bl => bl.binId)
```

### Bins' `reserveX` and `reserveY`

We need the `reserveX` and `reserveY` for each bin in `userPositionIds`. You can get this either by using the subgraph or interfacing directly with the contract through Ethers.js as shown below:

```js
// init LBPair contract
const lbPairContract = new Contract(
  lbPairAddr,
  LBPairV21ABI, // LBPairABI if it's a V2 pair
  PROVIDER
)

// Fetch bin reserves
interface BinReserves {
  reserveX: BigNumber;
  reserveY: BigNumber;
}
const binsReserves: BinReserves[] = await Promise.all(
  userPositionIds.map((binId) => lbPairContract.getBin(binId))
)
```

### LBToken totalSupply for each bin

Finally we need the LBToken `totalSupply` for each bin. Again, either through the subgraph or Ethers.js

```js
const totalSupplies: BigNumber[] = await Promise.all(
  userPositionIds.map((binId) => lbPairContract.totalSupply(binId))
)
```

## 3. Grant LBRouter access to your LBTokens
 
```js
const spender = LB_ROUTER_V21_ADDRESS[CHAIN_ID]

const estimatedGas = await lbPairContract.estimateGas.setApprovalForAll(
  spender,
  true
)

await lbPairContract.setApprovalForAll(
  spender,
  true,
  { gasLimit: calculateGasMargin(estimatedGas) }
)
```
## 4. Prepare removeLiquidity parameters

### Get `liquidityToRemove` 

Now we specify how much liquidity in each bin we'd like to remove. Let's say we want to remove 50% of the liquidity across all bins:

```js
// 50%
const frac = new Fraction( 
  JSBI.BigInt(50),
  JSBI.BigInt(100)
)

// compute liquidityToRemove
const liquidityToRemove: string[] = userBinLiquidities.map((bl) => {
  const liq = JSBI.BigInt(bl.liquidity)
  const liqToRemove = frac.multiply(liq)
  return liqToRemove.quotient.toString()
})
```

### Set amount slippage tolerance and get minimum amounts to remove

When removing liquidity, we can specify the minimum token amounts we expect to withdraw. This is because there could be amount slippages as the bins' `reserveX`, `reserveY` and `totalLiquidity` are constantly changing as others users swap or add/remove liquidity.

```js
// set amounts slippage tolerance; 0.5% in this example 
const userSlippageTolerance = new Percent(
  JSBI.BigInt(50),
  JSBI.BigInt(10000)
)

// get the amounts to remove
const {
  amountX, // amount of USDC expecting to remove
  amountY, // amount of USDCe expecting to remove
  amountXMin, // min amount of USDC to remove, calculated based on 'userSlippageTolerance'
  amountYMin // min amount of USDCe to remove
}:{
  amountX: JSBI
  amountY: JSBI
  amountXMin: JSBI
  amountYMin: JSBI
} = lbPairContract.calculateAmountsToRemove(
  userPositionIds,
  activeBinId,
  binsReserves,
  totalSupplies,
  liquidityToRemove,
  userSlippageTolerance
)
```

Note that you can set `userSlippageTolerance` to 0% if you don't want tolerate any slippage. 

## 5. Set removeLiquidity parameters
```js
// set transaction deadline
const currenTimeInSec =  Math.floor((new Date().getTime()) / 1000)
const daedline = currenTimeInSec + 3600

// set array of remove liquidity parameters
const removeLiquidityParams = [
  USDC.address,
  USDC_E.address,
  binStep,
  amountXMin.toString(),
  amountYMin.toString(),
  userPositionIds,
  liquidityToRemove,
  ACCOUNT,
  deadline.toHexString()
]
```

Note that `removeLiquidityParams` will look different for the `removeLiquidityAVAX` method. Please refer to this [link](/versioned_docs/version-V2.1/guides/add-remove-liquidity.md#removing-liquidity) for specific details.

## 6. Execute removeLiquidity contract call
```js
// init router contract
const routerContract = new Contract(
  LB_ROUTER_ADDRESS[CHAIN_ID],
  LBRouterABI,
  SIGNER
)

// set methods
const estimate = router.estimateGas.removeLiquidity
const method = router.removeLiquidity

// execute
const estimatedGasLimit = await estimate(...removeLiquidityParams)
await method(...removeLiquidityParams, {
  gasLimit: calculateGasMargin(estimatedGasLimit)
})
``` 