## Overview

The `createSpeedUpSend` API is responsible for initiating a speed up send operation.

## Params

The `CreateSpeedUpSendParams` used to initialize and perform `createSpeedUpSend` API.

- transaction hash: the transaction hash used to identify the transaction to speed up and for retrieving available send operation info
- fee per byte: the fee per byte to be paid to speed up transaction. See also [fetchSpeedUpAvailableFees API](FetchSpeedUpAvailableFees.md)

## Result

The newly created [SendResult](SendResult.md). 

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