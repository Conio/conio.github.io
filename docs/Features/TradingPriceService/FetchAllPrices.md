# Fetch All Prices

## Overview

`fetchAllUnitPrices` API is used to retrieve information about all tradable cryptocurrencies current unit prices values.

## Params

The `FetchAllUnitPricesParams` used to initialized and perform `fetchAllUnitPrices` API.

- fiat currency: the fiat currency used to fetch the pricing information

## Result

The `UnitPricesResult` data with all tradable cryptocurrencies current unit prices values.

- current prices: the current unit prices data and values `CurrentPrice` list

## Code

### iOS
```swift
let params = FetchAllUnitPricesParams.makeEuro()

tradingPriceService
    .fetchAllUnitPrices(with: params)
    .asPublisher()
    .sink { result in
        // ...
    }
```

### Android
```kotlin
conio.tradingPriceService
    .fetchAllUnitPrices()
    .asFlow()
    .collect { result ->
        // ...
    }
```