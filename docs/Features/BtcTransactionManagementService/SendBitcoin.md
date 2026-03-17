# Send Bitcoin 

## Overview

`send` API is used to send Bitcoin to a recipient. It allows client to send Bitcoin to a recipient based on an already created send operation. Upon success result, the send operation is taken in charge and the progress can be checked through the [fetchSend API](FetchSend.md)

## Params

The `SendParams` used to initialized and perform `send` API.

- send id: the send operation unique identifier
- mfa: multi-factor authentication info necessary to finalize the sell.

## Result

Success or error.

## Code

### iOS
```swift
let params = SendParams.make(
    sendId: ...,
    mfaParams: ...
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
val mfaParams = MfaParams(
    mfaToken = "...",
    code = "..."
)

val params = SendParams(
    sendId = "...",
    mfaParams = mfaParams
)

conio.btcTransactionService
    .send(params)
    .asFlow()
    .collect { result ->
        // ...
    }
```