# Buy

## Overview
---
`buy` API is used to execute the cryptocurrency purchase based on a specified bid quotation and crypto signature request. It allows client to specify the bid identifier and the signature request to execute and finalize purchase operation.

## Params
---
The `BuyParams` used to initialized and perform `buy` API.

- bid id: the existing bid identifier used to execute and finalize the purchase operation
- crypto request: the crypto signature used to validate the purchase operation

## Result
---
Success or error.

## Code
---
### iOS
```swift
let cryptoRequest = BuyParams.CryptoRequest
    .make(
        proofId: ...,
        expiration: ...,
        cryptoProof: ...
    )      
    
let params = BuyParams
    .make(
        bidId: ...,
        cryptoRequest: cryptoRequest
    )

tradingBuyService
    .buy(with: params)
    .asPublisher()
    .sink { result in
        // ..,
    }
```

### Android
```kotlin
val cryptoRequest = BidCryptoRequest(
    cryptoProof = ...,
    proofId = ...,
    expiration = ...,
)

val params = BuyParams(
    bidId = "...",
    cryptoRequest = cryptoRequest
)

conio.buyService
    .buy(params)
    .asFlow()
    .collect { result ->
        // ...
    }
```