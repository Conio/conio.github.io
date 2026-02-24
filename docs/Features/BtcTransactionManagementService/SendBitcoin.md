# Send Bitcoin 

## Overview

`send` API is used to send Bitcoin to a recipient. It allows client to send Bitcoin to a recipient based on the wallet destination address, the BTC amount to send and the fee per byte to be paid for the transaction.

## Params

The `SendParams` used to initialized and perform `send` API.

- send id: the send operation unique identifier
- mfa: multi-factor authentication info necessary to finalize the sell.

## Result

The [SendResult](SendResult.md) with the updated `status`

## Code

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
    amount = amount,
    feePerByte = CryptoAmount(...),
    addressBookId: "...",
    walletAddressId: "...",
)

conio.btcTransactionService
    .send(params)
    .asFlow()
    .collect { result ->
        // ...
    }
```