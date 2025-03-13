# Service categories

The Conio SDK provides a suite of modular services tailored to specific functionalities. These include wallet management, trading capabilities, and secure authentication. Each module offers the flexibility to integrate cryptocurrency features seamlessly into existing mobile applications.

## User Service

The `UserService` contains all the APIs used to manage a Conio user.

- [Login](./UserService/Login.md)
- [Signup](./UserService/Signup.md)
- [Logout](./UserService/Logout.md)
- [FetchLegalAcceptances](./UserService/FetchLegalAcceptances.md)
- [FetchPermissions](./UserService/FetchPermissions.md)
- [AcceptNewLegalAcceptances](./UserService/AcceptNewLegalAcceptances.md)

## Wallet Service

The `WalletService` contains all the APIs that provides information about the user wallet, such balance and mnemonic.

- [FetchBalances](./WalletService/FetchBalances.md)
- [FetchMnemonic](./WalletService/FetchMnemonic.md)

## Activities Service

The `ActivitiesService` contains all the API that provides information about wallet transactions.

- [FetchActivities](./ActivitiesService/FetchActivities.md)
- [FetchActivity](./ActivitiesService/FetchActivity.md)

## Trading Price Service

The `TradingPriceService` contains all the APIs that provides cryptocurrencies trading price information. It provides methods for fetching current or historical crypto prices and tradable metadata, including cryptocurrency ids.

- [FetchPrice](./TradingPriceService/FetchPrice.md)
- [FetchHistoricalPrice](./TradingPriceService/FetchHistoricalPrice.md)
- [FetchAllPrices](./TradingPriceService/FetchAllPrices.md)
- [FetchTradableCryptocurrenciesMetadata](./TradingPriceService/FetchTradableCryptocurrenciesMetadata.md)

## Trading Info Service

The `TradingInfoService` contains all the APIs used to manage a Conio user trading profile and information.

- [FetchTradingFees](./TradingInfoService/FetchTradingFees.md)
- [FetchTradingSummary](./TradingInfoService/FetchTradingSummary.md)
- [FetchTradingLimits](./TradingInfoService/FetchTradingLimits.md)
- [FetchTradingReport](./TradingInfoService/FetchTradingReport.md)

## BTC Transaction Service

The `BtcTransactionService` contains all the APIs responsible for managing Bitcoin transactions, including sending bitcoin, receiving bitcoin and speeding up transactions.

- [FetchAddress](./BtcTransactionManagementService/FetchAddress.md)
- [SendBitcoin](./BtcTransactionManagementService/SendBitcoin.md)
- [SpeedUpTransaction](./BtcTransactionManagementService/SpeedUpTransaction.md)
- [FetchTransactionAvailableFees](./BtcTransactionManagementService/FetchTransactionAvailableFees.md)
- [FetchSpeedUpAvailableFees](./BtcTransactionManagementService/FetchSpeedUpAvailableFees.md)

## Buy Service

The `BuyService` contains all the APIs designed to facilitate the purchase of cryptocurrencies through trading operations. It provides methods for creating, updating, fetching and finalizing bid quotations.

- [CreateBid](./TradingBuyService/CreateBid.md)
- [UpdateBid](./TradingBuyService/UpdateBid.md)
- [FetchBid](./TradingBuyService/FetchBid.md)
- [Buy](./TradingBuyService/Buy.md)

## Sell Service

The `SellService` contains all the APIs designed to facilitate the sale of cryptocurrencies through trading operations. It provides methods for creating, updating, fetching and finalizing ask quotations.

- [CreateAsk](./TradingSellService/CreateAsk.md)
- [UpdateAsk](./TradingSellService/UpdateAsk.md)
- [FetchAsk](./TradingSellService/FetchAsk.md)
- [Sell](./TradingSellService/Sell.md)

## Swap Service

The `SwapService` contains all the APIs designed to facilitate the cryptocurrency swap functionality. It provides methods for creating, updating, fetching and finalizing swap quotations between cryptos.

- [CreateSwap](./SwapService/CreateSwap.md)
- [UpdateSwap](./SwapService/UpdateSwap.md)
- [FetchSwap](./SwapService/FetchSwap.md)
- [Swap](./SwapService/Swap.md)

## Transfer Service

The `TransferService` contains all the APIs designed to facilitate the cryptocurrency amount transferring from an On-Chain Wallet to an Off-Chain Wallet of the same cryptocurrency and viceversa. It provides methods for creating, updating, fetching and finalizing transfer cryptocurrency between On-Chain and Off-Chain Wallet.

- [CreateTransfer](./TransferService/CreateTransfer.md)
- [UpdateTransfer](./TransferService/UpdateTransfer.md)
- [FetchTransfer](./TransferService/FetchTransfer.md)
- [Transfer](./TransferService/Transfer.md)