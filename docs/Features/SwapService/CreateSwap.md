# Create Swap

## Overview
---
`createSwap` API is used to create swap quotation details between two specified cryptocurrencies. It allows client to specify the source cryptocurrency, the destination cryptocurrency and the source cryptocurrency amount to exchange.

## Params
---
The `CreateSwapParams` used to initialized and perform `createSwap` API.

- source crypto id: the source cryptocurrency identifier used to create the swap operation
- destination crypto id: the destination cryptocurrency identifier used to create the swap operation
- source amount: the source cryptocurrency amount used to create the swap

## Result
---
- [Swap Result](SwapResult.md)

## Code
---
### iOS
```swift
let params = CreateSwapParams
    .make(
        sourceCryptoId: "cBTC",
        destinationCryptoId: "cETH",
        sourceCryptoAmount: .max
    )

swapService
    .createSwap(with: params)
    .asPublisher()
    .sink { result in
        // ...
    }
```

### Android
```kotlin
(TBD)
```