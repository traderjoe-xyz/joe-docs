---
sidebar_position: 1
sidebar_label: Making a Trade
---

# Making a Trade

This guide demonstrates how to execute a swap. In this example, we will be swapping 20 USDC for AVAX.

## 1. Required imports for this guide

```js
import {
  ChainId,
  WNATIVE,
  Token,
  TokenAmount,
  Percent,
} from "@traderjoe-xyz/sdk-core";
import {
  PairV2,
  RouteV2,
  TradeV2,
  TradeOptions,
  LB_ROUTER_V21_ADDRESS,
  jsonAbis,
} from "@traderjoe-xyz/sdk-v2";
import {
  createPublicClient,
  createWalletClient,
  http,
  parseUnits,
  BaseError,
  ContractFunctionRevertedError,
} from "viem";
import { privateKeyToAccount } from "viem/accounts";
import { avalanche } from "viem/chains";
import { config } from "dotenv";
```

## 2. Declare required constants

```js
config();
const privateKey = process.env.PRIVATE_KEY;
const { LBRouterV21ABI } = jsonAbis;
const CHAIN_ID = ChainId.AVALANCHE;
const router = LB_ROUTER_V21_ADDRESS[CHAIN_ID];
const account = privateKeyToAccount(`0x${privateKey}`);
```

Note that in your project, you most likely will not hardcode the private key at any time. You would be using libraries like [web3react](https://github.com/Uniswap/web3-react) or [wagmi](https://wagmi.sh/) to connect to a wallet, sign messages, interact with contracts, and get the above constants.

```js
// initialize tokens
const WAVAX = WNATIVE[CHAIN_ID]; // Token instance of WAVAX
const USDC = new Token(
  CHAIN_ID,
  "0xB97EF9Ef8734C71904D8002F8b6Bc66Dd9c48a6E",
  6,
  "USDC",
  "USD Coin"
);
const USDT = new Token(
  CHAIN_ID,
  "0x9702230A8Ea53601f5cD2dc00fDBc13d4dF4A8c7",
  6,
  "USDT",
  "Tether USD"
);

// declare bases used to generate trade routes
const BASES = [WAVAX, USDC, USDT];
```

## 3. Create Viem clients

```js
const publicClient = createPublicClient({
  chain: avalanche,
  transport: http(),
});

const walletClient = createWalletClient({
  account,
  chain: avalanche,
  transport: http(),
});
```

## 4. Declare user inputs and initialize `TokenAmount`

```js
// the input token in the trade
const inputToken = USDC;

// the output token in the trade
const outputToken = WAVAX;

// specify whether user gave an exact inputToken or outputToken value for the trade
const isExactIn = true;

// user string input; in this case representing 20 USDC
const typedValueIn = "20";

// parse user input into inputToken's decimal precision, which is 6 for USDC
const typedValueInParsed = parseUnits(typedValueIn, inputToken.decimals);

// wrap into TokenAmount
const amountIn = new TokenAmount(inputToken, typedValueInParsed);
```

## 5. Use PairV2 and RouteV2 functions to generate all possible routes

```js
// get all [Token, Token] combinations
const allTokenPairs = PairV2.createAllTokenPairs(
  inputToken,
  outputToken,
  BASES
);

// init PairV2 instances for the [Token, Token] pairs
const allPairs = PairV2.initPairs(allTokenPairs);

// generates all possible routes to consider
const allRoutes = RouteV2.createAllRoutes(allPairs, inputToken, outputToken);
```

## 6. Generate TradeV2 instances and get the best trade

```js
const isNativeIn = false; // set to 'true' if swapping from Native; otherwise, 'false'
const isNativeOut = true; // set to 'true' if swapping to Native; otherwise, 'false'

// generates all possible TradeV2 instances
const trades = await TradeV2.getTradesExactIn(
  allRoutes,
  amountIn,
  outputToken,
  isNativeIn,
  isNativeOut,
  publicClient,
  CHAIN_ID
);

// chooses the best trade
const bestTrade: TradeV2 = TradeV2.chooseBestTrade(trades, isExactIn);
```

## 7. Check trade information

```js
// print useful information about the trade, such as the quote, executionPrice, fees, etc
console.log(bestTrade.toLog());

// get trade fee information
const { totalFeePct, feeAmountIn } = await bestTrade.getTradeFee();
console.log("Total fees percentage", totalFeePct.toSignificant(6), "%");
console.log(`Fee: ${feeAmountIn.toSignificant(6)} ${feeAmountIn.token.symbol}`);
```

## 8. Declare slippage tolerance and swap method/parameters

```js
// set slippage tolerance
const userSlippageTolerance = new Percent("50", "10000"); // 0.5%

// set swap options
const swapOptions: TradeOptions = {
  allowedSlippage: userSlippageTolerance,
  ttl: 3600,
  recipient: account.address,
  feeOnTransfer: false, // or true
};

// generate swap method and parameters for contract call
const {
  methodName, // e.g. swapExactTokensForNATIVE,
  args, // e.g.[amountIn, amountOut, (pairBinSteps, versions, tokenPath) to, deadline]
  value, // e.g. 0x0
} = bestTrade.swapCallParameters(swapOptions);
```

## 9. Execute trade using Viem

Remember to approve spending ERC20 tokens by router before execution

```js
const { request } = await publicClient.simulateContract({
  address: router,
  abi: LBRouterV21ABI,
  functionName: methodName,
  args: args,
  account,
  value: BigInt(value),
});
const hash = await walletClient.writeContract(request);
console.log(`Transaction sent with hash ${hash}`);
```
