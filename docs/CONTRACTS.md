# Contracts

These references identify WormSwap's current BNB Smart Chain mainnet deployment.

| Network field | Value |
| --- | --- |
| Network | BNB Smart Chain mainnet |
| Chain ID | `56` |
| Native gas asset | BNB |
| Block explorer | [BscScan](https://bscscan.com) |
| Registry | [bsc-mainnet.json](../contracts/bsc-mainnet.json) |

## WormSwap Router

[`0x532Bd585DdB129ea50b0938995d3ac3184c4F1BC`](https://bscscan.com/address/0x532Bd585DdB129ea50b0938995d3ac3184c4F1BC#code)

The router executes supported swaps through allowed PancakeSwap V2/V3 integrations. It supports native/token input flows, route execution, and BNB/WBNB wrapping paths. It checks transaction parameters such as deadlines and minimum output, and collects the fixed `FEE_BPS = 20` router fee on actual received input.

- [Deployment transaction](https://bscscan.com/tx/0x1ee007745a97b3586bed37b84357262d8b320c1c9c06e3f8f0b6d0a83a60e115)
- Deployment block: `127956960`
- Deployment time: `2026-10-16 09:47:24 UTC`
- Inspect the `feeDistributor` and `wrappedNative` getters through BscScan.

The `SwapExecuted` event records a completed operation's trader, integration router, input/output assets, actual input, nominal router fee and received output. A route can contain several underlying hops while producing one completed-route event.

## WormFeeDistributor

[`0x66f87B4125b314a8Abd26AbCa7B43da045700Eb5`](https://bscscan.com/address/0x66f87B4125b314a8Abd26AbCa7B43da045700Eb5#code)

The collector receives router fees and accumulates them for TANUKI buybacks and burns. Its deployed `BURN_BPS = 10000` constant assigns the fee allocation to the burn cycle. Authorized keepers process native/token batches within configured thresholds, trade limits, deadlines and price safeguards.

Fees can accumulate between processing transactions. Collector balances, nominal router fees, purchased TANUKI and net tokens reaching the burn address are different quantities; see [Fee and Burn Mechanics](FEES-AND-BURNS.md).

## Asset references

| Asset | Mainnet address | Purpose |
| --- | --- | --- |
| TANUKI | [`0x77a9fdeaDA4D273Dc17374106Ee5121d9FCe7777`](https://bscscan.com/token/0x77a9fdeaDA4D273Dc17374106Ee5121d9FCe7777) | Ecosystem token and buyback/burn target |
| WBNB | [`0xbb4CdB9CBd36B01bD1cBaEBF2De08d9173bc095c`](https://bscscan.com/token/0xbb4CdB9CBd36B01bD1cBaEBF2De08d9173bc095c) | Wrapped representation of native BNB |
| Burn address | [`0x000000000000000000000000000000000000dEaD`](https://bscscan.com/address/0x000000000000000000000000000000000000dEaD) | Destination for processed TANUKI burns |

## Inspection and security

BscScan provides the published contract source and on-chain activity. Source verification establishes a link between published code and a deployment; it is not an independent security audit. Operational permissions and live configuration should be inspected on the deployed contracts.

Deployment references were checked against the project package and recorded on-chain reads on **18 October 2026**. Consult current explorer state for mutable settings.

[Back to WormSwap](../README.md)
