# Fetch Historical Prices

## Overview
---
`fetchHistoricalPrices` API is used to retrieve information about a specific cryptocurrency past time interval price value. It allows client to specify the cryptocurrency, the time frame and the time interval to fetch the cryptocurrency historical price points, analytics and time interval.

## Params
---
The `FetchHistoricalPricesParams` used to initialized and perform `fetchHistoricalPrices` API.

- crypto id: the cryptocurrency identifier used to retrieve the specific cryptocurrency historical price data
- time frame: the time frame in the past used to retrieve the specific cryptocurrency historical price data
- price interval: the price time interval used to retrieve the specific cryptocurrency historical price data

## Result
---
The `HistoricalPricesResult` data with cryptocurrency historical prices values. 

- cryptocurrency: the Wallet `Cryptocurrency`
- price points: the cryptocurrency historical price points
- price analytics: the cryptocurrency historical analytics
- interval: the cryptocurrency time interval

## Code
---
### iOS
```swift
let params = FetchHistoricalPricesParams
    .make(
        cryptoId: ...,
        timeFrame: .makeUsingLastDay(),
        priceInterval: .fifteenMinutes
    )
    
tradingPriceService
    .fetchHistoricalPrices(with: params)
    .asPublisher()
    .sink { result in
        // ...
    }
```

### Android
```kotlin
val oneDayInMillis = 24L * 60 * 60 * 1000
val timeFrame = TimeFrame(
    fromTimeInMillis = TimeFrame.now() - oneDayInMillis,
    toTimeInMillis = TimeFrame.now(),
)

val params = FetchHistoricalPricesParams(
    cryptoId = ...,
    timeFrame = timeFrame,
    priceInterval = PriceSamplingInterval.MINUTES_15,
)

conio.tradingPriceService
    .fetchHistoricalPrices(params)
    .asFlow()
    .collect { result ->
        // ...
    }
```