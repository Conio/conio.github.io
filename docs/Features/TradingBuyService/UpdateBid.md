# Update Bid

## Overview
---
`updateBid` API is used to update an existing bid for purchasing a cryptocurrency. It allows client to specify either the amount as crypto amount or fiat amount it is willing to update the bid, given its identifier.

## Params
---
The `UpdateBidParams` used to initialized and perform `updateBid` API.

- bid id: the existing bid identifier used to update the selected bid
- new amount: the new bid amount intended either as fiat amount or cryptocurrency amount

## Result
---
- [BidResult](BidResult.md)

## Code
---
### iOS
```swift
let params = UpdateBidParams
    .make(
        bidId: ..., 
        newAmount: ...
    )
tradingBuyService
    .updateBid(with: params)
    .asPublisher()
    .sink { result in
        // ...
    }
```

### Android
```kotlin
(TBD)
```