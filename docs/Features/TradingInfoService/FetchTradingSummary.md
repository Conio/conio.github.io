# Fetch Trading Summary

## Overview
---
`fetchTradingSummary` API is used to retrieve the trading stats and info linked to Conio user. It allows client to fetch the trading info involved in the Conio user trading operations.

## Parameters
---
The `FetchTradingSummaryParams` used to initialized and perform `fetchTradingSummary` API.

- fiat currency: The fiat currency used to fetch trading limits

## Result
---
The `TradingSummaryResult` trading stats and info involved in the Conio user trading operations.

- buy info: the trading buy stats
- sell info: the trading sell stats

## Code
---
### iOS
```swift
let params = FetchTradingSummaryParams.make()

tradingInfoService
	.fetchTradingSummary(with: params)
	.asPublisher()
	.sink { result in 
		...
	}
```

### Android
```kotlin
conio.tradingInfoService
	.fetchTradingSummary()
	.asFlow()
	.collect { result ->
		// ...
	}
```