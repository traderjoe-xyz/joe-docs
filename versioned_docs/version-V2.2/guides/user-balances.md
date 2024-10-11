---
sidebar_position: 11
sidebar_label: User balances
---

import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

# User balances
Swap fees are increasing reserves, without modifying user LBToken balances. 
There are few ways to fetch user's reserves, based on their holdings.


To calculate user's reserves, user's LBToken balance, total supply of LBToken and reserves in given bin are needed.

```
userReserveX = totalReserveX * userLBTokenBalance / totalSupply
userReserveY = totalReserveY * userLBTokenBalance / totalSupply
```

This needs to be calculated separately for every bin.

## Liquidity helper contract

Easiest and most straightforward way includes calling `getBinsReserveOf` function of liquidity helper contract.

When called with `id = 0` argument, it will fetch X bins around active bin (200 in example below).

<Tabs>
<TabItem value="python" label="Python" default>

```python
helper_contract = w3.eth.contract(address=liq_helper, abi=helper_abi)
result_tuple = helper_contract.functions.getBinsReserveOf(
    pool_address, user_address, 0, 200, 200
).call()
user_data = result_tuple[1]
user_tokenX = 0
user_tokenY = 0
for bin_id, reserveX, reserveY, shares, total_shares in user_data:
    tokenX_reserves = reserveX * shares / total_shares
    tokenY_reserves = reserveY * shares / total_shares
    user_tokenX += tokenX_reserves
    user_tokenY += tokenY_reserves
    print(
        f"User has {tokenX_reserves} of tokenX and {tokenY_reserves} of tokenY in bin {bin_id}"
    )
print(f"User has {user_tokenX} of tokenX and {user_tokenY} of tokenY in total")
```

</TabItem>
<TabItem value="javascript" label="Javascript" default>

```javascript
const client = createPublicClient({
  chain: avalanche,
  transport: http(),
});

const helperContract = {
  address: liqHelperAddress,
  abi: helperAbi,
};

async function getUserTokens() {
  try {
    const resultTuple = await client.readContract({
      address: helperContract.address,
      abi: helperContract.abi,
      functionName: 'getBinsReserveOf',
      args: [poolAddress, userAddress, 0, 200, 200],
    });

    const userData = resultTuple[1];
    let userTokenX = 0n;
    let userTokenY = 0n;

    for (const { id, reserveX, reserveY, shares, totalShares } of userData) {
      const tokenXReserves = (reserveX * shares) / totalShares;
      const tokenYReserves = (reserveY * shares) / totalShares;
      userTokenX += tokenXReserves;
      userTokenY += tokenYReserves;

      console.log(`User has ${tokenXReserves} of tokenX and ${tokenYReserves} of tokenY in bin ${id}`);
    }

    console.log(`User has ${userTokenX} of tokenX and ${userTokenY} of tokenY in total`);
  } catch (error) {
    console.error('Error fetching user tokens:', error);
  }
}

getUserTokens();
```

</TabItem>
</Tabs>

This method has disadvantage: if it isn't known, where liquidity was added, and bin id moved a lot since, not all bins might be covered.

## Using public API


<Tabs>
<TabItem value="python" label="Python" default>

```python
helper_contract = w3.eth.contract(address=liq_helper, abi=helper_abi)
header = {"x-traderjoe-api-key": "YOUR_KEY_LOADED_SECURELY"}
url = f"https://api.lfj.dev/v1/user/bin-ids/{user_address}/{chain}/{pool_address}"
result = requests.get(url, headers=header)
user_ids = result.json()

result_tuple = helper_contract.functions.getAmountsOf(
    pool_address, user_address, user_ids
).call()

tokenX_amounts = result_tuple[0]
tokenY_amounts = result_tuple[1]

print(
    f"User has {sum(tokenX_amounts)} of tokenX and {sum(tokenY_amounts)} of tokenY in total"
)
```

</TabItem>
<TabItem value="javascript" label="Javascript" default>

```javascript
const client = createPublicClient({
  chain: avalanche,
  transport: http(),
});

const apiKey = 'YOUR_KEY_LOADED_SECURELY';
const baseUrl = 'https://api.lfj.dev/v1/user/bin-ids';

async function getUserBinIds() {
  const url = `${baseUrl}/${userAddress}/avalanche/${poolAddress}`;
  const headers = {
    'x-traderjoe-api-key': apiKey,
  };
  const response = await fetch(url, { headers });
  const userIds = await response.json();
  return userIds;
}

async function getTokenAmounts(userIds) {
    const resultTuple = await client.readContract({
      address: liqHelperAddress,
      abi: helperAbi,
      functionName: 'getAmountsOf',
      args: [poolAddress, userAddress, userIds],
    });

    const tokenXAmounts = resultTuple[0]; 
    const tokenYAmounts = resultTuple[1]; 
    const totalTokenX = tokenXAmounts.reduce((acc, amount) => acc + amount, 0n);
    const totalTokenY = tokenYAmounts.reduce((acc, amount) => acc + amount, 0n);

    console.log(`User has ${totalTokenX} of tokenX and ${totalTokenY} of tokenY in total`);
}

async function main() {
    const userIds = await getUserBinIds();
    await getTokenAmounts(userIds);
}

main();
```

</TabItem>
</Tabs>

