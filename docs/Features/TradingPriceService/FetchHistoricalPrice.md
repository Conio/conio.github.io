# Fetch Historical Prices

## Overview

`fetchHistoricalPrices` API is used to retrieve information about a specific cryptocurrency past time interval price value. It allows client to specify the cryptocurrency, the time frame and the time interval to fetch the cryptocurrency historical price points, analytics and time interval.

## Params

The `FetchHistoricalPricesParams` used to initialized and perform `fetchHistoricalPrices` API.

- crypto id: the cryptocurrency identifier used to retrieve the specific cryptocurrency historical price data
- time frame: the available time frames used to retrieve the specific cryptocurrency historical price data
- fiat currency: the fiat currency used to retrieve historical price data

## Result

The `HistoricalPricesResult` data with cryptocurrency historical prices values. 

- cryptocurrency: the Wallet `Cryptocurrency`
- price points: the cryptocurrency historical price points
- price analytics: the cryptocurrency historical analytics

## Code

### iOS
```swift
let params = FetchHistoricalPricesParams
    .make(
        cryptoId: ...,
        timeFrame: .max,
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
val timeFrame = FetchHistoricalPricesParams.TimeFrame.Max

val params = FetchHistoricalPricesParams(
    cryptoId = ...,
    timeFrame = timeFrame,
)

conio.tradingPriceService
    .fetchHistoricalPrices(params)
    .asFlow()
    .collect { result ->
        // ...
    }
```