---
sidebar_position: 0
sidebar_label: Introduction
---

# Introduction

SDK-V2 is an open source library created to help builders interact with the V2, V2.1 and v2.2 contracts from their JS/TS projects. Please note that SDK-V2 is built on top of SDK-V1 so both libraries must be installed together. 

This guide endeavors to show examples of how builders can use the SDKs, together with [Viem](https://viem.sh/docs/getting-started.html), to perform a trade and add/remove liquidity.

## Installation

Run one of the following commands to add the required dependencies to your project:

### NPM
```
npm install @traderjoe-xyz/sdk @traderjoe-xyz/sdk-v2 @traderjoe-xyz/sdk-core viem
```

### Yarn
```
yarn add @traderjoe-xyz/sdk @traderjoe-xyz/sdk-v2 @traderjoe-xyz/sdk-core viem
```

## Classes
SDK-V2 implements 4 main classes: `PairV2`, `RouteV2`, `TradeV2`, and `Bin`. Specific documentation of the fields and functions for each class can be found in the code.

* [PairV2](https://github.com/traderjoe-xyz/joe-sdk-v2/blob/main/src/v2entities/pair.ts)
* [RouteV2](https://github.com/traderjoe-xyz/joe-sdk-v2/blob/main/src/v2entities/route.ts)
* [TradeV2](https://github.com/traderjoe-xyz/joe-sdk-v2/blob/main/src/v2entities/trade.ts)
* [Bin](https://github.com/traderjoe-xyz/joe-sdk-v2/blob/main/src/v2entities/bin.ts)

## Github
SDK-V2 uses Github to track issues and feature requests. Please open an issue if you have found a bug or have new feature requests. We also welcome contributions from the open source community. Open a pull request with a detailed explanation and the team will gladly review your contribution.

| Repo | Github URL |  NPM URL |
| :-------: | :----: | :----: |
| V2 | https://github.com/traderjoe-xyz/joe-sdks |  https://www.npmjs.com/package/@traderjoe-xyz/sdk-v2 |

