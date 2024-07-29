---
sidebar_position: 2
sidebar_label: Adding Liquidity
---

# Adding Liquidity

This guide shows how to add liquidity into a LBPair using the SDKs and viem. In this example, we will be adding 20 USDC and 20 USDC.e into a LBPair of USDC/USDC.e/1bps

## 1. Required imports and constants for this guide

### imports
```js
import { ChainId, Token, TokenAmount } from '@traderjoe-xyz/sdk-core'
import { PairV2, LB_ROUTER_V21_ADDRESS, jsonAbis, LiquidityDistribution, getLiquidityConfig, getUniformDistributionFromBinRange } from '@traderjoe-xyz/sdk-v2'
import { createPublicClient, createWalletClient, http, parseUnits, BaseError, ContractFunctionRevertedError } from 'viem'
import { privateKeyToAccount } from 'viem/accounts'
import { avalanche } from 'viem/chains'
import JSBI from 'jsbi'
import { config } from 'dotenv';
```

### Constants: chain and wallet
```js
config();
const privateKey = process.env.PRIVATE_KEY;
const { LBRouterV21ABI } = jsonAbis
const CHAIN_ID = ChainId.AVALANCHE
const router = LB_ROUTER_V21_ADDRESS[CHAIN_ID]
const account = privateKeyToAccount(`0x${privateKey}`)
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

const BIN_STEP = "1"
```

## 2. Create Viem clients
```js
const publicClient = createPublicClient({
    chain: avalanche,
    transport: http()
})

const walletClient = createWalletClient({
    account,
    chain: avalanche,
    transport: http()
})
```

## 3. Initialize user inputs
```js
// set the amounts for each of tokens 
const typedValueUSDC = "20"
const typedValueUSDCe = "20"

// wrap into TokenAmount
const typedValueUSDCParsed = parseUnits(
    typedValueUSDC,
    USDC.decimals
)
const typedValueUSDCeParsed = parseUnits(
    typedValueUSDCe,
    USDC.decimals
)
const tokenAmountUSDC = new TokenAmount(USDC, typedValueUSDCParsed)
const tokenAmountUSDCe = new TokenAmount(USDC_E, typedValueUSDCeParsed)

// set amounts slippage tolerance
const allowedAmountsSlippage = 50 // in bips, 0.5% in this case

// based on the amounts slippage tolerance, get the minimum amounts 
const minTokenAmountUSDC = JSBI.divide(
  JSBI.multiply(tokenAmountUSDC.raw, JSBI.BigInt(10000 - allowedAmountsSlippage)),
  JSBI.BigInt(10000)
)
const minTokenAmountUSDCe = JSBI.divide(
  JSBI.multiply(tokenAmountUSDCe.raw, JSBI.BigInt(10000 - allowedAmountsSlippage)),
  JSBI.BigInt(10000)
)

// set deadline for the transaction
const currentTimeInSec = Math.floor((new Date().getTime()) / 1000)
const deadline = currenTimeInSec + 3600
```

## 4. Get the LBPair's active bin
```js
const pair = new PairV2(USDC, USDC_E)
const binStep = Number(BIN_STEP)
const isV21 = true
const lbPair = await pair.fetchLBPair(binStep, isV21, publicClient, CHAIN_ID)
if (lbPair.LBPair == "0x0000000000000000000000000000000000000000") {
    console.log("No LB pair found with given parameters")
    return
}
const lbPairData = await PairV2.getLBPairReservesAndId(lbPair.LBPair, isV21, publicClient)
const activeBinId = lbPairData.activeId
```

## 5. Get addLiquidity parameters
```js
// Example 1: getting distribution parameters for one of the default 'LiquidityDistribution' shapes 
const { deltaIds, distributionX, distributionY } = getLiquidityConfig(LiquidityDistribution.SPOT)

// Example 2: getting distribution parameters for uniform distribution given a price range
const binRange = [activeBinId - 10, activeBinId + 10]
const { deltaIds, distributionX, distributionY } = getUniformDistributionFromBinRange(
    activeBinId,
    binRange,
    [tokenAmountUSDC, tokenAmountUSDCe]
)

// declare liquidity parameters
const addLiquidityInput = {
  tokenX: USDC_E.address,
  tokenY: USDC.address,
  binStep: Number(BIN_STEP),
  amountX: tokenAmountUSDC.raw.toString(),
  amountY: tokenAmountUSDCe.raw.toString(),
  amountXMin: minTokenAmountUSDC.toString(),
  amountYMin: minTokenAmountUSDCe.toString(),
  activeIdDesired: activeBinId,
  idSlippage: 5,
  deltaIds,
  distributionX,
  distributionY,
  to: account.address,
  refundTo: account.address,
  deadline: currentTimeInSec + 3600
}
```
For additional details about the parameters, refer to this [link](/versioned_docs/version-V2.2/guides/add-remove-liquidity.md#liquidity-parameters). 


## 6. Execute addLiquidity contract call
```js
const { request } = await publicClient.simulateContract({
    address: router,
    abi: LBRouterV21ABI,
    functionName: "addLiquidity",
    args: [addLiquidityInput],
    account
})
const hash = await walletClient.writeContract(request)
console.log(`Transaction sent with hash ${hash}`)
```