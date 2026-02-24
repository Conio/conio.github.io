# Create Send

## Overview

`createSend` API is responsible for managing Bitcoin send transactions

# Params

The `CreateSendParams` used to initialize and perform `createSend` API. 

- destination address: the recipient's wallet address
- fee per byte: the fee rate used for the transaction
- amount: the crypto amount to send without the fees
- address book id: the unique identifier of send address
- wallet address id: the unique identifier of send wallet

## Result

The [SendResult](SendResult.md) with the updated `status`. 

### Android
```kotlin

val params = FetchSendParams(
    sendId: "send_id_1",
)

conio.btcTransactionService
    .fetchSend(params)
    .asFlow()
    .collect {
        // ...
    }

```