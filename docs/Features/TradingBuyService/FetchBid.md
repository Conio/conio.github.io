# Fetch Bid

## Overview

`fetchBid` API is used to retrieve information about a specific cryptocurrency bid. It allows client to specify the bid identifier to fetch the specific purchase quotation with information such as crypto amount and fiat amount.

## Params

The `FetchBidParams` used to initialize and perform `fetchBid` API.

- bid id: the existing bid identifier used to retrieve the specific bid quotation

## Result

- [BidResult](BidResult.md)

## Code

### iOS
```swift
let params = FatchBidParams.make(bidId: ...)

tradingBuyService
    .fetchBid(with: params)
    .asPublisher()
    .sink { result in
        // ...
    }
```

### Android
```kotlin
val params = FetchBidParams(
    bidId = "..."
)

conio.buyService
    .fetchBid(params)
    .asFlow()
    .collect { result ->
        // ...
    }
```