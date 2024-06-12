# Update Ask

## Overview
---
`updateAsk` API is used to update an existing ask for selling a cryptocurrency. It allows client to specify either the amount as crypto amount, fiat amount or max sellable amount it is willing to update the ask given its identifier.

## Params
---
The `UpdateAskParams` used to initialized and perform `updateAsk` API.

- ask id: the existing ask identifier used to update the selected ask
- amount: the new ask amount intended either as fiat amount, cryptocurrency amount or max sellable amount

## Result
---
- [AskResult](AskResult.md)

## Code
---
### iOS
```swift
let params = UpdateAskParams
    .make(
        askId: ..., 
        newAmount: ...
    )
    
tradingSellService
    .updateAsk(with: params)
    .asPublisher()
    .sink { result in
        // ...
    }
```

### Android
```kotlin
(TBD)
```