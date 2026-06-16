# Create Send

## Overview

`createSend` API is responsible for initiating a send operation, it allows client to define the send operation details and obtain important informations, e.g. the total amount of mining fee to pay or the exchange value of cryptocurrency.

# Params

The `CreateSendParams` used to initialize and perform `createSend` API. 

- destination address: the recipient's wallet address
- fee per byte: the fee rate used for the transaction. See also [fetchTransactionAvailableFees API](FetchTransactionAvailableFees.md)
- amount: the crypto amount intended either as cryptocurrency amount to send or max sendable amount (fees included)
- address book id: the unique identifier of recipient address book entry, it could be omitted if the send operation is a UTXO consolidation
- wallet address id: the unique identifier of wallet address entry saved in address book, it could be omitted if the send operation is a UTXO consolidation

## Result

The newly created [SendResult](SendResult.md). 

## Code

### iOS
```swift
let params = CreateSendParams.make(
    destinationAddress: ...,
    amount: ...,
    feePerByte: ...,
    addressBookId: ...,
    walletAddressId: ...
)

btcTransactionManagementService
    .createSend(with: params)
    .asPublisher()
    .sink { result in
        // ...
    }
```

### Android
```kotlin

val walletAddress = "..."

// val amount = AmountParams.Max
val amount = AmountParams.Crypto(
    value = CryptoAmount(...)
)

val params = CreateSendParams(
    destinationAddress = walletAddress,
    feePerByte = CryptoAmount(...),
    amount = amount,
    addressBookId = "..."?,
    walletAddressId = "..."?,
)

conio.btcTransactionService
    .createSend(params)
    .asFlow()
    .collect {
        // ...
    }
```