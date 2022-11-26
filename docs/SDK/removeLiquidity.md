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
  LB_ROUTER_ADDRESS,
  LBRouterABI,
  LBPairABI,
} from '@traderjoe-xyz/sdk-v2'
import { Token } from '@traderjoe-xyz/sdk'
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

Note that in your project, you most likely will not hardcode the private key at any time. You would be using libraries like [web3react](https://github.com/Uniswap/web3-react) or [wagmi](https://wagmi.sh/) to connect to a wallet, sign messages, interact with contracts, and get the values for PROVIDER, SIGNER and ACCOUNT

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

The following data needs to be fetched to compute the amount of USDC and USDC.e currently deposited in the USDC/USDC.e/2bps LBPair. This is because the the pooled token amounts will constantly change depending on the current active bin, and the bins' reserveX/Y and totalSupply. 

Please note that this step will be significantly simplified in the future with the support of the **LiquidityAmounts** periphery contract in SDK-V2.  

### LBPair and active bin

```js
const pair = new PairV2(USDC, USDC_E)
const binStep = Number(BIN_STEP)

const lbPair = await pair.fetchLBPair(binStep, PROVIDER, CHAIN_ID)
const lbPairAddr = lbPair.LBPair

const lbPairData = await PairV2.getLBPairReservesAndId(lbPair.LBPair, PROVIDER)
const activeBinId = lbPairData.activeId.toNumber()
```

### Liquidity positions 

Use the [subgraph](https://docs.traderjoexyz.com/subgraphs/avalanche) to fetch your positions. You need all the `binId`s where you have liquidity and the amount of `liquidity` in each bin. Below is an example of a GraphQL query to the subgraph's `LiquidityPositions` entity.
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

We'll assume you have fetched your positions from the subgraph, resulting in `UserBinPosition[]` as the following:

```js
interface UserBinPosition {
  binId: string
  liquidity: string
}

let userBinLiquidities: UserBinPosition[]

// array of binIds where user has liquidity
const userPositionIds: string[] = userBinLiquidities.map(bl => bl.binId)
```

### Bins' reserveX and reserveY

We need the reserveX and reserveY for each `userPositionIds`. You can get this either by using the subgraph or interfacing directly with the contract through Ethers.js

```js

// init LBPair contract
const lbPairContract = new Contract(
  lbPairAddr,
  LBPairABI,
  PROVIDER
)

// Fetch bin reserves
interface BinReserves {
  reserveX: BigNumber;
  reserveY: BigNumber;
}
const binsReserves: BinReserves[] = await Promise.all(
  userPositionIds.map((binId) => pairContract.getBin(binId))
)
```

### LBToken totalSupply for each bin

Finally we need the LBToken totalSupply for each bin. Again, either through the subgraph or Ethers.js

```js
const totalSupplies: BigNumber[] = await Promise.all(
  userPositionIds.map((binId) => pairContract.totalSupply(binId))
)
```

## 3. Prepare removeLiquidity parameters

### Set `liquidityToRemove` 

Now we specify how much liquidity in each bin you'd like to remove. Let's say we want to remove 50% of the liquidity across all bins:

```js
const liquidityToRemove: string[] = userBinLiquidities.map((bl) => {
  const liq = JSBI.BigInt(bl.liquidity)
  const frac = new Fraction( // 50%
    JSBI.BigInt(50),
    JSBI.BigInt(100)
  )
  const liqToRemove = frac.multiply(liq)
  return liqToRemove.quotient.toString()
})
```

### Set amount slippage tolerance and get minimum amounts to remove

When removing liquidity, we can specify the minimum token amounts we expect to withdraw. This is because there could be amount slippages as the bins' reserveX, reserveY and totalLiquidity continue changing.

```js
// set amounts slippage tolerance; 0.5% in this example 
const userSlippageTolerance = new Percent(
  JSBI.BigInt(50),
  JSBI.BigInt(10000)
)

// get the amounts to remove
const {
  amountX, // amount of USDC to remove
  amountY, // amount of USDCe to remove
  amountXMin, // min amount of USDC to remove
  amountYMin // min amount of USDCe to remove
}:{
  amountX: JSBI
  amountY: JSBI
  amountXMin: JSBI
  amountYMin: JSBI
} = pair.calculateAmountsToRemove(
  userPositionIds,
  activeBinId,
  binsReserves,
  totalSupplies,
  liquidityToRemove,
  userSlippageTolerance
)
```

## 4. Set removeLiquidity parameters and execute contract call
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

Note that `removeLiquidityParams` will look different for the `removeLiquidityAVAX` method. Please refer to this [link](https://docs.traderjoexyz.com/guides/manage-a-liquidity-position#removing-liquidity) for specific details.