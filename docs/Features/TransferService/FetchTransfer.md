# Fetch Transfer

## Overview

`fetchTransfer` API is used to retrieve information about a specific transfer. It allows client to specify the transfer identifier to fetch the specific transfer quotation with information such as the source cryptocurrency, source cryptocurrency amount, destination cryptocurrency, gross crypto amount and fees.

## Params

The `FetchTransferParams` used to initialized and perform `fetchTransfer` API.

- transfer id: the existing transfer identifier used to retrieve the specific transfer quotation

## Result

- [TransferResult](TransferResult.md)

## Code

### iOS
```swift
let params = FetchTransferParams.make(transferId: ...) 

transferService
    .fetchTransfer(with: params)
    .asPublisher()
    .sink { result in
        // ...
    }
```

### Android
```kotlin
val params = FetchTransferParams(
    transferId = "...",
)

conio.transferService
    .fetchTransfer(params)
    .asFlow()
    .collect {
        // ...
    }
```