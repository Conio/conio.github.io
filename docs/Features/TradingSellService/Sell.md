# Sell

## Overview

`sell` API is used to execute the cryptocurrency selling based on a specified ask quotation and crypto signature request. It allows client to specify the ask identifier and the signature request to execute and finalize selling operation.

## Params

The `SellParams` used to initialized and perform `sell` API.

- ask id: the existing ask quotation identifier used to execute and finalize the sell operation
- crypto request: the crypto signature used to validate the sell operation
- wait until paid: prevent the service to complete until the ask is not in `paid` status (or in another end status, like `charged` or `error`)

## Result

The [AskResult](AskResult.md) with the updated `status`. If the `status` is different from `paid` or `charged`, the transaction can still end with an error (use the [Fetch Ask service](FetchAsk.md) to keep checking the status).

## Code

### iOS
```swift
let cryptoRequest = SellParams.CryptoRequest
    .make(
        proofId: ...,
        expiration: ...,
        cryptoProof: ...
    )

let params = SellParams
    .make(
        askId: ...,
        cryptoRequest: cryptoRequest
    )

tradingSellService
    .sell(with: params)
    .asPublisher()
    .sink { result in
        // ...
    }
```

### Android
```kotlin
val cryptoRequest = SellCryptoRequest(
    cryptoProof = ...,
    proofId = ...,
    expiration = ...,
)

val params = SellParams(
    askId = "...",
    cryptoRequest = cryptoRequest,
)

conio.sellService
    .sell(params)
    .asFlow()
    .collect { result ->
        // ...
    }
```