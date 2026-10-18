# Features

## Swap Terminal

The terminal brings token selection, route quotes, pool charts and observed trading activity into one BNB Chain interface. Supported execution paths use PancakeSwap V2/V3 liquidity. Availability depends on the selected assets, supported routes, pool liquidity and token behavior.

The selected quote includes the WormSwap router fee. Pool fees, price impact, slippage, network gas and applicable token taxes can also affect the result. Review the final wallet request and execution parameters before authorizing a transaction.

## Shareable asset selections

The swap page supports these query parameters:

| Parameter | Accepted selection | Example |
| --- | --- | --- |
| `inputCurrency` | Native `BNB` or a BEP20 contract address | `BNB` |
| `outputCurrency` | Native `BNB` or a BEP20 contract address | TANUKI's contract address |

Example: [open BNB → TANUKI](https://wormswap.finance/swap?inputCurrency=BNB&outputCurrency=0x77a9fdeada4d273dc17374106ee5121d9fce7777).

For a different BEP20 asset, use its BNB Chain contract address in the relevant parameter. A link preselects assets; it does not authorize a purchase. Unknown assets require token metadata resolution. Invalid addresses or identical input/output selections produce a selection error.

## Personal token imports

Custom token imports are stored in the user's browser. Importing a token does not add it to another user's default token list or establish an official listing. A separate browser or cleared storage can have a different import list.

## Market and wallet tools

| Tool | Purpose | Coverage |
| --- | --- | --- |
| Token Explorer | Token reports, liquidity, market information and contract details | Data depends on available chain and market sources |
| Whale Radar | Observed larger trades and token activity | Thresholds and available indexed trades determine visibility |
| Holder Rewards | Supported token reward/dividend information | Token-specific support; not a universal rewards claim service |
| WormShield | Review and manage supported token allowances | Wallet discovery and token/spender coverage can vary |

## Network and wallets

WormSwap's current swap deployment targets **BNB Smart Chain mainnet, chain ID 56**. It integrates wagmi, viem and Reown AppKit to connect supported wallets. Wallet applications display and authorize transaction requests in their own interface.

[Back to WormSwap](../README.md)
