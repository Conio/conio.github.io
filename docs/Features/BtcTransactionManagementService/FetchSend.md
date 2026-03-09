# Fetch Send

## Overview

`fetchSend` API fetches the send operation info. It allows client to obtain send information based on the send identifier.

## Params

The `FetchSendParams` used to initialize and perform `fetchSend` API.

- send id: the transaction hash to use for retrieving available send operation info

## Result

The [SendResult](SendResult.md) with the updated `status`. 

## Code

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