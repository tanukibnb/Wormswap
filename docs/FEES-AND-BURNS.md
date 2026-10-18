# Fee and Burn Mechanics

WormSwap charges a fixed **0.20% router fee** on the input actually received by the router. The current fee collector assigns its fee allocation entirely to the TANUKI buyback and burn cycle.

## Fee calculation

```text
router fee = floor(actual received input × 20 / 10,000)
route input = actual received input − router fee
```

For an illustrative **1 BNB** input received by the router, the WormSwap fee is **0.002 BNB**, leaving **0.998 BNB** for route execution. This example isolates the WormSwap fee; the resulting output also depends on liquidity, underlying pool fees, execution prices, applicable token taxes and gas.

For a transfer-taxed input token, the amount the router actually receives can differ from the wallet's requested amount. The collector's credited token amount can also be smaller than the nominal fee if that fee transfer is taxed.

## From fees to burn

1. Successful router operations send fees to the deployed WormFeeDistributor.
2. Balances accumulate until an eligible processing batch is available.
3. An authorized keeper submits a processing transaction with the required route, output bounds and deadline.
4. The collector checks configured batch/trade limits and price protections before conversion.
5. The resulting net TANUKI is transferred to `0x000000000000000000000000000000000000dEaD`.

The collector's `BURN_BPS = 10000` constant means the fee allocation is **100% for the burn cycle**. It does not mean 100% of a user's trade is burned. Processing is batched, so collection and a subsequent buyback/burn can occur at different times.

## Reading on-chain quantities

| Quantity | What it represents |
| --- | --- |
| Actual input | Asset amount received by the WormSwap router |
| Nominal router fee | Fee amount calculated by the router |
| Collector receipt | Native/token amount actually credited to the fee collector |
| Purchased TANUKI | Output of a processing conversion |
| Net burned TANUKI | Increase recorded at the designated burn address from the burn transfer |

These values can differ because of asset units, prices and token transfer taxes. Aggregate values across different assets require appropriate token decimals and pricing.

## Tracking the cycle

Inspect the [router](https://bscscan.com/address/0x532Bd585DdB129ea50b0938995d3ac3184c4F1BC#code), [collector](https://bscscan.com/address/0x66f87B4125b314a8Abd26AbCa7B43da045700Eb5#code) and their transaction histories. The current implementation records completed swaps, native fee receipts and processed burns through contract events.

[Back to WormSwap](../README.md)
