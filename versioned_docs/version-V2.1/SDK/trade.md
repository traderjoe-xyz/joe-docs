---
sidebar_position: 1
sidebar_label: Making a Trade 
---

# Making a Trade 

This guide demonstrates how to execute a swap. In this example, we will be swapping 20 USDC for AVAX.

## 1. Required imports for this guide
```js
import { PairV2, RouteV2, TradeV2, LB_ROUTER_V21_ADDRESS, LBRouterV21ABI } from '@traderjoe-xyz/sdk-v2'
import { Token, ChainId, WNATIVE, TokenAmount, JSBI, Percent} from '@traderjoe-xyz/sdk'
import { Wallet } from 'ethers'
import { Contract } from '@ethersproject/contracts'
import { parseUnits } from '@ethersproject/units'
import { JsonRpcProvider } from '@ethersproject/providers'
```

## 2. Declare required constants
```js
const AVAX_URL = 'https://api.avax.network/ext/bc/C/rpc'
const CHAIN_ID = ChainId.AVALANCHE
const PROVIDER = new JsonRpcProvider(AVAX_URL)
const WALLET_PK = "{WALLET_PRIVATE_KEY}"
const SIGNER = new Wallet(WALLET_PK, PROVIDER)
const ACCOUNT = await SIGNER.getAddress()
```
Note that in your project, you most likely will not hardcode the private key at any time. You would be using libraries like [web3react](https://github.com/Uniswap/web3-react) or [wagmi](https://wagmi.sh/) to connect to a wallet, sign messages, interact with contracts, and get the above constants.

```js
// initialize tokens
const WAVAX = WNATIVE[CHAIN_ID] // Token instance of WAVAX
const USDC = new Token(
    CHAIN_ID,
    '0xB97EF9Ef8734C71904D8002F8b6Bc66Dd9c48a6E',
    6,
    'USDC',
    'USD Coin'
)
const USDT = new Token(
    CHAIN_ID,
    '0x9702230A8Ea53601f5cD2dc00fDBc13d4dF4A8c7',
    6,
    'USDT',
    'Tether USD'
)

// declare bases used to generate trade routes
const BASES = [WAVAX, USDC, USDT] 
```

## 3. Declare user inputs and initialize `TokenAmount`
```js
// the input token in the trade
const inputToken = USDC

// the output token in the trade
const outputToken = WAVAX

// specify whether user gave an exact inputToken or outputToken value for the trade
const isExactIn = true

// user string input; in this case representing 20 USDC
const typedValueIn = '20' 

// parse user input into inputToken's decimal precision, which is 6 for USDC
const typedValueInParsed = parseUnits( 
  typedValueIn, 
  inputToken.decimals
).toString() // returns 20000000

// wrap into TokenAmount
const amountIn = new TokenAmount(
  inputToken, 
  JSBI.BigInt(typedValueInParsed)
) 
```

## 4. Use PairV2 and RouteV2 functions to generate all possible routes
```js
// get all [Token, Token] combinations 
const allTokenPairs = PairV2.createAllTokenPairs(
  inputToken,
  outputToken,
  BASES
)

// init PairV2 instances for the [Token, Token] pairs
const allPairs = PairV2.initPairs(allTokenPairs) 

// generates all possible routes to consider
const allRoutes = RouteV2.createAllRoutes(
  allPairs,
  inputToken,
  outputToken,
  2 // maxHops 
) 
```

## 5. Generate TradeV2 instances and get the best trade
```js
const isAvaxIn = false // set to 'true' if swapping from AVAX; otherwise, 'false'
const isAvaxOut = true // set to 'true' if swapping to AVAX; otherwise, 'false'

// generates all possible TradeV2 instances
const trades = await TradeV2.getTradesExactIn(
  allRoutes,
  amountIn,
  outputToken,
  isAvaxIn,
  isAvaxOut, 
  provider,
  chainId
) 

// chooses the best trade 
const bestTrade: TradeV2 = TradeV2.chooseBestTrade(trades, isExactIn)
```

## 6. Check trade information
```js
// print useful information about the trade, such as the quote, executionPrice, fees, etc
console.log(bestTrade.toLog())

// get trade fee information
const { totalFeePct, feeAmountIn } = await bestTrade.getTradeFee(provider)
console.log('Total fees percentage', totalFeePct.toSignificant(6), '%')
console.log(`Fee: ${feeAmountIn.toSignificant(6)} ${feeAmountIn.token.symbol}`)
```

## 7. Declare slippage tolerance and swap method/parameters
```js
// set slippage tolerance
const userSlippageTolerance = new Percent(JSBI.BigInt(50), JSBI.BigInt(10000)) // 0.5%

// set deadline for the transaction
const currenTimeInSec =  Math.floor((new Date().getTime()) / 1000)
const daedline = currenTimeInSec + 3600

// set swap options
const swapOptions = {
  recipient: ACCOUNT, 
  allowedSlippage: userSlippageTolerance, 
  deadline,
  feeOnTransfer: false // or true
}

// generate swap method and parameters for contract call
const {
  methodName, // e.g. swapExactTokensForAVAX,
  args,       // e.g.[amountIn, amountOut, binSteps, path, to, deadline]
  value       // e.g. 0x0
} = bestTrade.swapCallParameters(swapOptions)

```
## 8. Execute trade using Ethers.js
```js
// init router contract
const router = new Contract(
  LB_ROUTER_V21_ADDRESS[CHAIN_ID],
  LBRouterV21ABI,
  SIGNER
)

// estimate gas
const gasOptions = value && !isZero(value) ? { value } : {} 
const gasEstimate = await router.estimateGas[methodName](...args, options)

// execute swap
const options = value && !isZero(value) 
  ? { value, from: ACCOUNT }
  : { from: ACCOUNT }
await router[methodName](...args, {
  gasLimit: calculateGasMargin(gasEstimate),
  ...options
})
```