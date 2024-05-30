# Speed Up Transaction 

## Overview
---
`speedUp` API is used to accelerate a pending Bitcoin transaction by increasing its fees. It allows client to speed up the transaction based on the transaction hash identifier and the new fee per byte to be paid for the transaction.

## Params
---
The `SpeedUpParams` used to initialized and perform `speedUp` API.

- transaction hash: the transaction hash to use for submit speed up
- fee per byte: the new fee per byte to be paid for submit speed up

## Result
---
The `SpeededUpTransactionResult` speeded up BTC transaction data.

- hash: the transaction hash identifier
- activity id: the Conio services transaction activity identifier

## Code
---
### iOS
```swift
let params = SpeedUpParams
    .make(
        transactionHash: ...,
        feePerByte: ...
    )
btcTransactionManagementService
    .speedUp(with: params)
    .asPublisher()
    .sink { result in
        // ...
    }
```

### Android
```kotlin
val params = SpeedUpParams(
    transactionHash = "...",
    feePerByte = CryptoAmount(...)
)

conio.btcTransactionService
    .speedUp(params)
    .asFlow()
    .collect { result ->
        // ...
    }
```