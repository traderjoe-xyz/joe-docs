---
sidebar_position: 3
sidebar_label: veJoe for Developers
---

# Joe V1

## veJOE for Developers


### Boosted APRs
With the introduction of Boosted MasterChef Joe (BMCJ), users now see different Boosted APRs depending on their veJOE balance. 
A users total farm APR now consist of 2 components: 

**Base APR**
Share of emissions that is not adjusted by veJOE: `total farm APR * (1 - veJoeShare)`

**Boost APR**
Determined by the user factor 
\frac{\sqrt{user.liquidity * user.veJoe} }{pool.totalFactor}  
where `pool.totalFactor` is the sum of all user factor in the farm. 
​
### FarmLensV2
To help with the calculation of Boost APR, developers can try our FarmLensV2: 
​​
#### Example

```
// ethers.Contract  
const farmLensContract = useFarmLensV2Contract()
​
// poolIds is an array e.g. [0,1,3,6]
const response = await farmLensContract?.getBMCJFarmInfos(
  masterchefAddress,
  account,
  poolIds
)
​
// APRs returned in 18 decimal
const baseAPR = response.baseAPR
const boostedAPR = response.

```

### Reference
​For more please refer to [Staking V2](https://github.com/traderjoe-xyz/research/blob/main/Joe%20Staking%20V2.pdf)