---
sidebar_position: 1
sidebar_label: V2.2 Key Changes
---

# V2.2 Key Changes

A summary of key changes in Liquidity Book V2.2: 
- Hooks are added to LBPair
- Core functionality stays the same, existing functions have signatures unchanged

### LBFactory
- Added functions to manage hooks on pairs (only LB_HOOKS_MANAGER_ROLE)

### LBPair 
- Added functions to manage hooks (only LBFactory)
- Added hooks on mint, burn, flashloan and transfer

### LBRouter
- `Versions` struct is extended to accomodate V2.2 paths

### LBQuoter
- Includes V2.2 paths

### LBHooksRewarders
- New contract utilizing hooks
- Rewards users that provide liquidity based on time spent in defined range around active bin