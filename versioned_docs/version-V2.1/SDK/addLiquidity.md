---
sidebar_position: 2
sidebar_label: Adding Liquidity
---

# Adding Liquidity

This guide shows how to add liquidity into a LBPair using the SDKs and Ethers.js. In this example, we will be adding 20 USDC and 20 USDC.e into a LBPair of USDC/USDC.e/2bps

## 1. Required imports and constants for this guide

### imports
```js
import { 
  LB_ROUTER_V21_ADDRESS, 
  LBRouterV21ABI,
  PairV2,
  Bin, 
  LiquidityDistribution, 
  getLiquidityConfig, 
  getDistributionFromTargetBin, 
  getUniformDistributionFromBinRange 
} from '@traderjoe-xyz/sdk-v2'
import { ChainId, Token, CurrencyAmount, JSBI } from '@traderjoe-xyz/sdk'
import { Wallet, BigNumber } from 'ethers'
import { MaxUint256 } from '@ethersproject/constants'
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

## 2. Approve the LBRouter to use your USDC and USDC.e tokens
```js
const spender = LB_ROUTER_V21_ADDRESS[CHAIN_ID]
const estimatedGas = await tokenContract.estimateGas.approve(spender, MaxUint256)
await tokenContract.approve(
  spender, 
  MaxUint256, 
  { gasLimit: calculateGasMargin(estimatedGas) } 
)
```
Note that the above requires you to have initialized `tokenContract: Contract` using the token address and the ERC20 ABI. Repeat this procedure twice: once for USDC and once for USDC.e

## 3. Initialize user inputs
```js
// set the amounts for each of tokens 
const typedValueUSDC = "20"
const typedValueUSDCe = "20"

// wrap into TokenAmount
const tokenAmountUSDC = new TokenAmount(USDC, JSBI.BigInt(typedValueUSDC))
const tokenAmountUSDCe = new TokenAmount(USDC_E, JSBI.BigInt(typedValueUSDCe))

// set amounts slippage tolerance
const allowedAmountsSlippage = 50 // in bips, 0.5% in this case

// based on the amounts slippage tolerance, get the minimum amounts 
const minTokenAmountUSDC =  JSBI.divide(
  JSBI.multiply(tokenAmountUSDC.raw, JSBI.BigInt(10000 - allowedAmountsSlippage)),
  JSBI.BigInt(10000)
)
const minTokenAmountUSDCe =  JSBI.divide(
  JSBI.multiply(tokenAmountUSDCe.raw, JSBI.BigInt(10000 - allowedAmountsSlippage)),
  JSBI.BigInt(10000)
)

// set price slippage tolerance
const allowedPriceSlippage = 50 // in bips, 0.5% in this case
const priceSlippage = allowedPriceSlippage / 10000 // 0.005

// set deadline for the transaction
const currenTimeInSec =  Math.floor((new Date().getTime()) / 1000)
const daedline = currenTimeInSec + 3600
```

## 4. Get the LBPair's active bin
```js
const pair = new PairV2(USDC, USDC_E)
const binStep = Number(BIN_STEP)
const isV21 = true // set to true if it's a V2.1 pair
const lbPair = await pair.fetchLBPair(binStep, isV21, PROVIDER, CHAIN_ID)
const lbPairData = await PairV2.getLBPairReservesAndId(lbPair.LBPair, isV21, PROVIDER)
const activeBinId = lbPairData.activeId
```

## 5. Get addLiquidity parameters
```js
// get idSlippage
const idSlippage = Bin.getIdSlippageFromPriceSlippage(
  priceSlippage,
  Number(BIN_STEP)
)

// Example 1: getting distribution parameters for one of the default 'LiquidityDistribution' shapes 
const { deltaIds, distributionX, distributionY } = getLiquidityConfig(LiquidityDistribution.NORMAL)

// Example 2: getting distribution parameters for uniform distribution given a price range
const binRange = [activeBinId-5, activeBinId+5]
const { deltaIds, distributionX, distributionY } = getUniformDistributionFromBinRange(
  activeBinId,
  binRange,
  [tokenAmountUSDC, tokenAmountUSDCe]
)

// Example 2: getting distribution parameters given a price target
const targetBin = activeBinId
const { deltaIds, distributionX, distributionY } = getUniformDistributionFromBinRange(
  activeBinId,
  targetBin,
)

// declare liquidity parameters
const addLiquidityInput = {
  tokenX: USDC.address,
  tokenY: USDC_E.address,
  binStep: Number(BIN_STEP),
  amountX: tokenAmountUSDC.raw.toString(),
  amountY: tokenAmountUSDCe.raw.toString(),
  amountXMin: minTokenAmountUSDC.toString(),
  amountYMin: minTokenAmountUSDCe.toString(),
  activeIdDesired: activeBinId,
  idSlippage,
  deltaIds,
  distributionX,
  distributionY,
  to: ACCOUNT,
  refundTo: ACCOUNT,
  deadline 
}
```
For additional details about the parameters, refer to this [link](/versioned_docs/version-V2.1/guides/add-remove-liquidity.md#liquidity-parameters). 


## 6. Execute addLiquidity contract call
```js
// init router contract
const router = new Contract(
  LB_ROUTER_V21_ADDRESS[CHAIN_ID],
  LBRouterV21ABI,
  SIGNER
)

// declare methods
const estimate = router.estimateGas.addLiquidity // 'addLiquidityAVAX' if one of the tokens is AVAX
const method = router.addLiquidity

// set AVAX amount, such as tokenAmountAVAX.raw.toString(), when one of the tokens is AVAX; otherwise, set to null
const value = null 

// call methods
const estimatedGasLimit = await estimate(
  addLiquidityInput,
  value ? { value } : {}
)
await method(addLiquidityInput, {
  ...(value ? { value } : {}),
  gasLimit: calculateGasMargin(estimatedGasLimit)
})
```