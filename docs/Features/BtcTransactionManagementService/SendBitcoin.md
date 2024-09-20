# Send Bitcoin 

## Overview
---
`send` API is used to send Bitcoin to a recipient. It allows client to send Bitcoin to a recipient based on the wallet destination address, the BTC amount to send and the fee per byte to be paid for the transaction.

## Params
---
The `SendParams` used to initialized and perform `send` API.

- destination address: the recipient BTC wallet address
- btc amount: the BTC amount to send. It can be a specific amount or the whole wallet spendable balance
- fee per byte: the fee per byte to be paid for the send transaction

## Result
---
The `SendTransactionResult` executed BTC send transaction data.

- hash: the transaction hash identifier
- activity id: the Conio services transaction activity identifier

## Code
---
### iOS
```swift
let params = SendParams
    .makeSendingExactAmount(
        cryptoAmountValue: ...,
        destinationAddress: ...,
        feePerByte: ...
    )
btcTransactionManagementService
    .send(with: params)
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

val params = SendParams(
    destinationAddress = "...",
    btcAmount = amount,
    feePerByte = CryptoAmount(...)
)

conio.btcTransactionService
    .send(params)
    .asFlow()
    .collect { result ->
        // ...
    }
```