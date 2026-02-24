## Overview

The `createSpeedUpSend` API is used to accelerate a pending send transaction by increasing its fees. It allows client to speed up the transaction based on the transaction hash identifier and the new fee per byte to be paid for the transaction.

## Params

The `CreateSpeedUpSendParams` used to initialize and perform `createSpeedUpSend` API.

- transaction hash: the transaction hash to use for retrieving available send operation info
- fee per byte: the fee per byte to be paid for the send transaction 

## Result

The [SendResult](SendResult.md) with the updated `status`

## Code 

### Android
```

val params = CreateSpeedUpSendParams(
    transactionHash: "transaction_hash_1",
    feePerByte: CryptoAmount(...),
)

conio.btcTransactionService
    .send(params)
    .asFlow()
    .single()

```