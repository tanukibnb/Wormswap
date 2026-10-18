# Architecture

WormSwap combines a browser-based trading interface, server-side data services and on-chain execution on BNB Smart Chain.

## Components

| Layer | Responsibility | Main technology |
| --- | --- | --- |
| Interface | Token selection, amounts, quotes, route display, charts and market tools | Next.js, React, TypeScript |
| Wallet integration | Connection, BNB Chain context and wallet-authorized requests | wagmi, viem, Reown AppKit |
| Application services | Token discovery, market data, chart history and tool responses | Next.js server routes, RPC and external data providers |
| Swap execution | Supported V2/V3 route execution, minimum-output and deadline checks, router fee collection | WormSwap Router, Solidity |
| Fee processing | Fee accumulation and controlled TANUKI buyback/burn batches | WormFeeDistributor, Solidity |

## A swap from quote to settlement

1. The user selects input/output assets and an input amount.
2. Route discovery examines supported PancakeSwap V2/V3 paths and obtains a quote.
3. The interface prepares transaction parameters, including the selected route, recipient, minimum output and deadline.
4. The wallet presents any required token approval and swap transaction to the user.
5. The router receives the input, collects its fee and executes the route through allowed liquidity integrations.
6. The output is delivered to the transaction's recipient; receipts and events provide the on-chain record.

Quotes describe an estimate at a point in time. Pool state, liquidity, token behavior and transaction ordering can change before execution. The router enforces the submitted transaction bounds.

## Market data and execution

Token reports, pool charts and observed trades provide information around a swap. They are supplied through application data services using chain reads and external market sources, including GeckoTerminal.

A chart update does not execute a trade. Swap settlement is determined by the signed on-chain transaction and its resulting receipt. Data coverage and refresh timing can vary by token, pool and provider.

## Fee processing

Swap fees flow to the collector separately from trade output. A keeper processes eligible accumulated batches under the collector's configured constraints. The resulting net TANUKI burn is recorded on-chain.

See [Fee and Burn Mechanics](FEES-AND-BURNS.md) and [Contracts](CONTRACTS.md).

## WormSwap Arena

Arena is a separate game application with its own client and server responsibilities. Its private development and settlement testing are outside the public swap execution path documented here. Paid public availability is tracked in [Project Status](PROJECT-STATUS.md).

[Back to WormSwap](../README.md)
