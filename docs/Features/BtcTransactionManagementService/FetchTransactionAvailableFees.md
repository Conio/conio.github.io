# Fetch Transaction Available Fees

## Overview
---
`fetchTransactionAvailableFees` API fetches the BTC available transaction fees. It allows client to obtain fee information based on the transaction crypto amount, transaction speed type and recipient wallet address.

## Params
---
The `FetchTransactionAvailableFeesParams` used to initialized and perform `fetchTransactionAvailableFees` API.

- btc amount: the transaction BTC crypto amount. It can be a specific amount or the whole wallet spendable balance
- transaction speeds: the transaction speeds types use to retrieve available fees
- destination address: the BTC recipient wallet address

## Result
---
The `BtcTransactionFeesResult` BTC available transaction fees data.

- available fees: the transaction available fees list with details

## Code
---
### iOS
```swift
let params = FetchTransactionAvailableFeesParams
    .makeForAllSpeeds(
        destinationAddress: ...,
        amount: .cryptoAmount(value: ...)
    )
btcTransactionManagementService
    .fetchTransactionAvailableFees(with: params)
    .asPublisher()
    .sink { result in
        // ...
    }
```

### Android
```kotlin
(TBD)
```