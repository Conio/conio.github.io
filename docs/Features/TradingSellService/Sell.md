# Sell

## Overview
---
`sell` API is used to execute the cryptocurrency selling based on a specified ask quotation and crypto signature request. It allows client to specify the ask identifier and the signature request to execute and finalize selling operation.

## Params
---
The `SellParams` used to initialized and perform `sell` API.

- ask id: the existing ask quotation identifier used to execute and finalize the sell operation
- crypto request: the crypto signature used to validate the sell operation

## Result
---
Success or error.

## Code
---
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
(TBD)
```