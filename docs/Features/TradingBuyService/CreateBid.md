# Create Bid

## Overview
---
`createBid` API is used to create a bid for purchasing a cryptocurrency. It allows client to specify either the amount as crypto amount or fiat amount it is willing to create the bid.

## Params
---
The `CreateBidParams` used to initialized and perform `createBid` API.

- crypto id: the cryptocurrency identifier used to create the bid quotation
- fiat currency: the bid fiat currency
- amount: the bid amount intended either as fiat amount or cryptocurrency amount

## Result
---
- [BidResult](BidResult.md)

## Code
---
### iOS
```swift
let params = CreateBidParams.makeBTC(amount: ...)

tradingBuyService
    .createBid(with: params)
    .asPublisher()
    .sink { result in
        // ...
    }
```

### Android
```kotlin
(TBD)
```