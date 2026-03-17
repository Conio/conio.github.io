# Update Send

## Overview

`updateSend` API is used to update an existing send operation that hasn't been already submitted. It allows client to specify either the amount as crypto amount and the fee per byte as crypto amount it is willing to update the send given its identifier.

# Params

The `RefreshSendParams` used to initialize and perform `refreshSend` API. 

- send id: the send identifier used to create the send operation
- fee per byte: the fee rate used for transaction
- mfa: multi-factor authentication params used to process the send operation

## Result

The [SendResult](SendResult.md).

## Code

### iOS
```swift
let params = UpdateSendParams.make(
    sendId: ...,
    amount: ...,
    feePerByte: ...
)

btcTransactionManagementService
    .updateSend(with: params)
    .asPublisher()
    .sink { result in
        // ...
    }
```

### Android
```
// val amount = AmountParams.Max
val amount = AmountParams.Crypto(
    value = CryptoAmount(...)
)

val params = UpdateSendParams(
    sendId = "...",
    feePerByte = CryptoAmount(...),
    amount = amount
)

conio.btcTransactionService
    .send(params)
    .asFlow()
    .collect {
        // ...
    }
```