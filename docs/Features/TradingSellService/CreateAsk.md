# Create Ask 

## Overview
---
`createAsk` API is used to create an ask for selling a cryptocurrency. It allows client to specify either the amount as crypto amount, fiat amount or max sellable amount it is willing to create the ask.

## Params
---
### 
The `CreateAskParams` used to initialized and perform `createAsk` API.

- crypto id: the cryptocurrency identifier used to create the ask quotation
- fiat currency: the ask fiat currency
- amount: the ask amount intended either as fiat amount, cryptocurrency amount or max sellable amount

## Result
---
- [AskResult](AskResult.md)

## Code
---
### iOS
```swift
let params = CreateAskParams.makeBTC(amount: ...)

tradingSellService
    .createAsk(with: params)
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

val params = CreateAskParams(
    cryptoId = "...",
    amount = amount,
)

conio.sellService
    .createAsk(params)
    .asFlow()
    .collect { result ->
        // ...
    }
```