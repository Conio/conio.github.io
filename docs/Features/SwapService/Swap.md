# Swap

## Overview
---
`swap` API is used to execute and finalize the exchange between two specified cryptocurrencies based on a specified swap quotation and crypto signature request. It allows client to specify the swap identifier and the signature request to execute and finalize swap operation.

## Params
---
The `SwapParams` used to initialized and perform `swap` API.

- swap id: the existing swap quotation identifier used to execute and finalize the swap operation
- crypto request: the crypto signature used to validate the swap operation
- wait until paid: prevent the service to complete until the swap is not in `paid` status (or in another end status, like `finalized` or `error`)

## Result
---
The [SwapResult](SwapResult.md) with the updated `status`. If the `status` is different from `paid` or `finalized`, the transaction can still end with an error (use the [Fetch Swap service](FetchSwap.md) to keep checking the status).

## Code
---
### iOS
```swift
(TBD)
```

### Android
```kotlin
(TBD)
```