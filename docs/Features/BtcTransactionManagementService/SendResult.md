# Send Result

## Overview

The `SendResult` with updated data used to execute a send operation.

## Properties

- sendId: the send operation unique identifier,
- crypto currency: the `Cryptocurrency` being sent
- crypto amount: the amount of crypto currency to send
- fiat amount: the exchange value of crypto currency in fiat
- fee per byte: the fee rate used for the transaction
- network fee: the total network fee paid for the transaction, in satoshi
- destination address: the recipient's wallet address
- address book id: the unique identifier of send address
- wallet address id:  the unique identifier of send wallet
- created at: the date when the send operation is created
- confirmed at: the date when the send operation is confirmed on blockchain
- transaction id: the blockchain transaction ID, available once the transaction is broadcasted
- status: the status that describes the send operation