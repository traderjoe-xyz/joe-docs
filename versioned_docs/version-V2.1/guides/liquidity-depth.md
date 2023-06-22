---
sidebar_position: 10
sidebar_label: Finding Liquidity Depth
---

# Finding Liquidity Depth

As Joe-v2 liquidity consists of reserves concentrated in different bins, price impact of a trade depends on how many bins are crossed during trades. Below code snippet shows, how to calculate +/-2 liquidity depth. In this case it is understood as amount of reserves, that need to leave pair, to move enough bins for price to change by +/-2%.

To change amount of percent, adjust `percent_depth` from `get_ids` function

Note, that for function `get_all_reserves()` Multicall usage is recommended due to amount of calls that will happen.

```python
import json
import math
from web3 import Web3
from typing import Tuple

# load ABIs
abisPath = "ABIS/"
with open(f"{abisPath}LBPairV21.json") as file:
    LBPair_ABI = json.load(file)
with open(f"{abisPath}ERC20_ABI.json") as file:
    ERC20_ABI = json.load(file)

# prepare web3
provider_url = "https://arbitrum-one.public.blastapi.io"
web3 = Web3(Web3.HTTPProvider(provider_url))
assert web3.isConnected(), "web3 is not connected"


def get_decimals(pairContract) -> Tuple[int, int]:
    tokenX_address = web3.toChecksumAddress(pairContract.functions.getTokenX().call())
    tokenY_address = web3.toChecksumAddress(pairContract.functions.getTokenY().call())
    tokenX_decimals = (
        web3.eth.contract(address=tokenX_address, abi=ERC20_ABI)
        .functions.decimals()
        .call()
    )
    tokenY_decimals = (
        web3.eth.contract(address=tokenY_address, abi=ERC20_ABI)
        .functions.decimals()
        .call()
    )
    return (tokenX_decimals, tokenY_decimals)


# multicall is recommended to use here, as this might make up to 400 calls for bin step = 1
def get_all_reserves(ids, pairContract) -> Tuple[list[int], list[int]]:
    bin_reserves_x = []
    bin_reserves_y = []
    for id in ids:
        reserve_x, reserve_y = pairContract.functions.getBin(id).call()
        bin_reserves_x.append(reserve_x)
        bin_reserves_y.append(reserve_y)
    return bin_reserves_x, bin_reserves_y


def get_ids(pairContract) -> list[int]:
    bin_step = pairContract.functions.getBinStep().call()
    active_bin = pairContract.functions.getActiveId().call()
    percent_depth = 200  # 200 = 2%
    """
    Example: for bin_step = 10 to lower a price by 2%, active bin needs to be moved by 20 bins:
    1) clearing active bin liqudity
    2) trading away 19 bins below
    3) trade at least 1 token from next bin - this will be ignored
    So in this case, there will be 39 bins taken into consideration
    For case bin step = 15 bins amount gets rounded up
    """
    bins_to_move_price = math.ceil(percent_depth / bin_step)

    start_bin = active_bin - bins_to_move_price + 1
    end_bin = active_bin + bins_to_move_price

    ids = [bin_id for bin_id in range(start_bin, end_bin)]
    return ids


if __name__ == "__main__":
    pair_address = web3.toChecksumAddress(
        "0x94d53BE52706a155d27440C4a2434BEa772a6f7C"
    )  # eth-usdc on Arbitrum

    pairContract = web3.eth.contract(address=pair_address, abi=LBPair_ABI)

    ids = get_ids(pairContract)

    bin_reserves_x, bin_reserves_y = get_all_reserves(ids, pairContract)

    tokenX_decimals, tokenY_decimals = get_decimals(pairContract)

    reserves_x_to_clear = sum(bin_reserves_x) / 10**tokenX_decimals
    reserves_y_to_clear = sum(bin_reserves_y) / 10**tokenY_decimals

    print("reserves_x_to_clear", reserves_x_to_clear)
    print("reserves_y_to_clear", reserves_y_to_clear)

```
