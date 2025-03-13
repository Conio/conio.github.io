# Transfer

## Overview

`transfer` API is used to execute and finalize the transfer operation of a cryptocurrency amount from On-Chain Wallet to the same cryptocurrency Off-Chain Wallet or viceversa. It allows client to specify the transfer identifier and the signature request to execute and finalize transfer operation.

## Params

The `TransferParams` used to initialized and perform `transfer` API.

- transfer id: the existing transfer quotation identifier used to execute and finalize the transfer quotation
- crypto request: the crypto signature used to validate the transfer quotation
- wait until paid: prevent the service to complete until the transfer is not in `paid` status (or in another end status, like `finalized` or `error`)

## Result

The [TransferResult](TransferResult.md) with the updated `status`. If the `status` is different from `paid` or `finalized`, the transaction can still end with an error (use the [Fetch Transfer service](FetchTransfer.md) to keep checking the status).

## Code

### iOS
```swift
let cryptoRequest = TransferParams.CryptoRequest
    .make(
        proofId: ...,
        expiration: ...,
        cryptoProof: ...
    )      
    
let params = TransferParams
    .make(
        transferId: ...,
        cryptoRequest: cryptoRequest
    )

transferService
    .transfer(with: params)
    .asPublisher()
    .sink { result in
        // ..,
    }
```

### Android
```kotlin
val cryptoRequest = TransferCryptoRequest(
    cryptoProof = ...,
    proofId = "...",
    expiration = ...,
)

val params = TransferParams(
    transferId = "...",
    cryptoRequest = cryptoRequest 
)

conio.transferService
    .transfer(params)
    .asFlow()
    .collect {
        // ...
    }
```