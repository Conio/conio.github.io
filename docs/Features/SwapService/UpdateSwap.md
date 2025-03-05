# Update Swap

## Overview

`updateSwap` API is used to update an existing swap quotation for exchange two specified cryptocurrencies. It allows client to specify the new source crypto amount it is willing to update the swap quotation given its identifier.

## Params

The `UpdateSwapParams` used to initialized and perform `updateSwap` API.

- swap id: the existing swap identifier used to update the selected swap quotation
- source amount: the new swap source crypto amount used to update the selected swap quotation

## Result

- [Swap Result](SwapResult.md)

## Code

### iOS
```swift
let params = UpdateSwapParams
    .make(
        swapId: ..., 
        newSourceAmount: ...
    )

swapService
    .updateSwap(with: params)
    .asPublisher()
    .sink { result in
        // ...
    }
```

### Android
```kotlin
// val amount = AmountParams.Max
val amount = AmountParams.Crypto(
    value = CryptoAmount(...)
)

val params = UpdateSwapParams(
    swapId = "...",
    sourceAmount = amount
)

conio.swapService
    .updateSwap(params)
    .asFlow()
    .collect {
        // ...
    }
```