# Fetch Speed Up Available Fees

## Overview
---
`fetchSpeedUpAvailableFees` API fetches the available speed up fees for accelerating a BTC transaction. It allows client to obtain fee information based on the transaction hash identifier for which it wants to accelerate.

## Params
---
The `FetchSpeedUpAvailableFeesParams` used to initialize and perform `fetchSpeedUpAvailableFees` API.

- transaction hash: the transaction hash to use for retrieving available speed up fees

## Result
---
The `BtcSpeedUpFeesResult` BTC available speed up fees data.

- available fees: the speedup available fees list with details
- transaction mempool status: the actual mempool status compared to the transaction

## Code
---
### iOS
```swift
let params = FetchSpeedUpAvailableFeesParams.make(transactionHash: ...)

btcTransactionManagementService
    .fetchSpeedUpAvailableFees(with: params)
    .asPublisher()
    .sink { result in
        // ...
    }
```

### Android
```kotlin
val params = FetchSpeedUpAvailableFeesParams(
    transactionHash = "...",
)

conio.btcTransactionService
    .fetchSpeedUpAvailableFees(params)
    .asFlow()
    .collect { result ->
        // ...
    }
```