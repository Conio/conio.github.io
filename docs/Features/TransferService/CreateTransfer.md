# Create Transfer 

## Overview
---
`createTransfer` API is used to create cryptocurrency amount transfer quotation details from On-Chain Wallet to the same cryptocurrency Off-Chain Wallet or viceversa. It allows client to specify the source cryptocurrency either On-Chain or Off-Chain, the destination same cryptocurrency either Off-Chain or On-Chain and the source cryptocurrency amount to transfer.

## Params
---
The `CreateTransferParams` used to initialized and perform `createTransfer` API.

- source crypto: the source cryptocurrency used to create the transfer quotation
- destination crypto: the destination cryptocurrency used to create the transfer quotation
- source amount: the source cryptocurrency amount used to create the transfer quotation

## Result
---
- [TransferResult](TransferResult.md)

## Code
---
### iOS
```swift
let params = CreateTransferParams
    .make(
        sourceCrypto: .onChainBtc,
        destinationCrypto: .offChainBtc,
        sourceCryptoAmount: .max
    )

transferService
    .createTransfer(with: params)
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

val params = CreateTransferParams(
    sourceCryptoId = "...",
    destinationCryptoId = "...",
    sourceAmount = amount
)

conio.transferService
    .createTransfer(params)
    .asFlow()
    .collect {
        // ...
    }
```