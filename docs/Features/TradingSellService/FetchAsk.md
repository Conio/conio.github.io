# Fetch Ask

## Overview
---
`fetchAsk` API is used to retrieve information about a specific ask. It allows client to specify the ask identifier to fetch the specific selling quotation with information such as crypto amount, fiat amount and fees.

## Params
---
The `FetchAskParams` used to initialized and perform `fetchAsk` API.

- ask id: the existing ask identifier used to retrieve the specific ask

## Result
---
- [AskResult](AskResult.md)

## Code
---
### iOS
```swift
let params = FatchAskParams.make(askId: ...)

tradingSellService
    .fetchAsk(with: params)
    .asPublisher()
    .sink { result in
        // ...
    }
```

### Android
```kotlin
(TBD)
```