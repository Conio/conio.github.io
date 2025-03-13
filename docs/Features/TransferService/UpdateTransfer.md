# Update Transfer 

## Overview

`updateTransfer` API is used to update an existing transfer quotation for transfer a cryptocurrency amount from On-Chain Wallet to the same cryptocurrency Off-Chain Wallet or viceversa. It allows client to specify the new source crypto amount it is willing to update the transfer quotation given its identifier.

## Params

The `UpdateTransferParams` used to initialized and perform `updateTransfer` API.

- transfer id: the existing transfer identifier used to update the selected transfer quotation
- source amount: the new transfer source crypto amount used to update the selected transfer quotation

## Result

- [TransferResult](TransferResult.md)

## Code

### iOS
```swift
let params = UpdateTransferParams
    .make(
        transferId: ...,
        newSourceAmount: ...
    )

transferService
    .updateTransfer(with: params)
    .asPublisher()
    .sink { result in
        // ...
    }
```

### Android
```kotlin
// val amount = AmountParams.Max
val amount = AmountParams.Crypto(
    value = CryptoAmount(...)
)

val params = UpdateTransferParams(
    transferId = "...",
    sourceAmount = amount
)

conio.transferService
    .updateTransfer(params)
    .asFlow()
    .collect {
        // ...
    }
```