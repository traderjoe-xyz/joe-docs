---
sidebar_position: 3
sidebar_label: Removing Liquidity
---

# Removing Liquidity

This guide shows how to remove liquidity from a V2.1 pool using the SDKs, and Viem. In this example, we will be removing liquidity from a LBPair of USDC/USDC.e/1bps

## 1. Required imports and constants for this guide

### Imports
```js
import { ChainId, Token } from '@traderjoe-xyz/sdk-core'
import { PairV2, LB_ROUTER_V21_ADDRESS, jsonAbis, } from '@traderjoe-xyz/sdk-v2'
import { getContract, createPublicClient, createWalletClient, http, BaseError, ContractFunctionRevertedError } from 'viem'
import { privateKeyToAccount } from 'viem/accounts'
import { avalanche } from 'viem/chains'
import { config } from 'dotenv';
```
### Constants: chain and wallet
```js
config();
const privateKey = process.env.PRIVATE_KEY;
const { LBRouterV21ABI, LBPairV21ABI } = jsonAbis
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


## 3. Getting data

### LBPair and active bin

```js
const pair = new PairV2(USDC, USDC_E)
const binStep = Number(BIN_STEP)
const pairVersion = 'v21'
const lbPair = await pair.fetchLBPair(binStep, pairVersion, publicClient, CHAIN_ID)
if (lbPair.LBPair == "0x0000000000000000000000000000000000000000") {
    console.log("No LB pair found with given parameters")
    return
}
const lbPairData = await PairV2.getLBPairReservesAndId(lbPair.LBPair, pairVersion, publicClient)
const activeBinId = lbPairData.activeId.toNumber()
```

### Liquidity positions 

Use the below code to fetch your positions directly from chain. You need all the `binId`s where you have liquidity and the amount of `liquidity` in each bin. 
```js
const pairContract = getContract({ address: lbPair.LBPair, abi: LBPairV21ABI })
const range = 200 // should be enough in most cases
const addressArray = Array.from({ length: 2 * range + 1 }).fill(account.address);
const binsArray = [];
for (let i = activeBinId - range; i <= activeBinId + range; i++) {
    binsArray.push(i);
}
const allBins: Bigint[] = await publicClient.readContract({
    address: pairContract.address,
    abi: pairContract.abi,
    functionName: 'balanceOfBatch',
    args: [addressArray, binsArray]
})
const userOwnedBins = binsArray.filter((bin, index) => allBins[index] != 0n);
const nonZeroAmounts = allBins.filter(amount => amount !== 0n);
```

Please take note, that we aren't fetching ERC20 token amounts underlying for this example. This results in using parameters amountXmin and amountYmin equal to zero. Calculating them would require additionally:
1. Fetch tokenSupply of all owned bins
2. Fetch reserves of all owned bins
3. Calculate reserves owned by user (ownedReserves * liquidityOwned / totalSupply)
4. Applying desired slippage to above.

This process will become easier, when public API is opened.

## 4. Grant LBRouter access to your LBTokens
 
```js
const approved = await publicClient.readContract({
    address: pairContract.address,
    abi: pairContract.abi,
    functionName: 'isApprovedForAll',
    args: [account.address, router]
})

if (!approved) {
    const { request } = await publicClient.simulateContract({
        address: pairContract.address,
        abi: pairContract.abi,
        functionName: 'approveForAll',
        args: [router, true],
        account
    })
    const hashApproval = await walletClient.writeContract(request)
    console.log(`Approving transaction sent with hash ${hashApproval}`)
}
```


## 5. Set removeLiquidity parameters
```js
// set transaction deadline
const currentTimeInSec =  Math.floor((new Date().getTime()) / 1000)

// set array of remove liquidity parameters
const removeLiquidityInput = {
    tokenX: USDC_E.address,
    tokenY: USDC.address,
    binStep: Number(BIN_STEP),
    amountXmin: 0,
    amountYmin: 0,
    ids: userOwnedBins,
    amounts: nonZeroAmounts,
    to: account.address,
    deadline: currentTimeInSec + 3600
}
```

Note that `removeLiquidityParams` will look different for the `removeLiquidityAVAX` method. Please refer to this [link](/versioned_docs/version-V2.1/guides/add-remove-liquidity.md#removing-liquidity) for specific details.

## 6. Execute removeLiquidity contract call
```js
const { request } = await publicClient.simulateContract({
    address: router,
    abi: LBRouterV21ABI,
    functionName: "removeLiquidity",
    args: [
        removeLiquidityInput.tokenX,
        removeLiquidityInput.tokenY,
        removeLiquidityInput.binStep,
        removeLiquidityInput.amountXmin, //zero in this example
        removeLiquidityInput.amountYmin, //zero in this example
        removeLiquidityInput.ids,
        removeLiquidityInput.amounts,
        removeLiquidityInput.to,
        removeLiquidityInput.deadline],
    account
})
const removalHash = await walletClient.writeContract(request)
console.log(`Transaction sent with hash ${removalHash}`)
``` 