# Fetch Price

## Overview
---
`fetchPrice` API is used to retrieve information about a specific cryptocurrency current price value. It allows client to specify either the cryptocurrency current unit price or a specific cryptocurrency amount to fetch the current buy, sell and raw prices values.

## Params
---
The `FetchPriceParams` used to initialized and perform `fetchPrice` API.

- crypto id: the cryptocurrency unique identifier used to fetch the current price
- type: the price type intended either as cryptocurrency current unit price or current price for a specific cryptocurrency amount

## Result
---
The `PriceResult` data with cryptocurrency current price values. 

- current price: the current price data and values `CurrentPrice`

## Code
---
### iOS
```swift
let params = FetchPriceParams.makeUnitCurrenPrice(cryptoId: "cADA")

tradingPriceService
	.fetchPrice(params: params)
	.asPublisher()
	.sink { result in 
		// ...
	}
```

### Android
```kotlin

```