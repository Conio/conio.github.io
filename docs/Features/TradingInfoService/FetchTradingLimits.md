# Fetch Trading Limits

## Overview
---
`fetchTradingLimits` API is used to retrieve the trading limits linked to Conio user. It allows client to fetch the trading limits involved in the Conio user trading operations.

## Parameters
---
The `FetchTradingLimitsParams` used to initialized and perform `fetchTradingLimits` API.

- fiat currency: The fiat currency used to fetch trading limits

## Result
---

The `TradingLimitsResult` trading limits info involved in the Conio user trading operations.

- sell limits: the crypto trading sell limits
- buy limits: the crypto trading buy limits

## Code
---
### iOS

```swift
let params = FetchTradingLimitsParams.make()

tradingInfoService
	.fetchTradingLimits(with: params)
	.asPublisher()
	.sink { result in 
		...
	}
```

### Android
```kotlin
conio.tradingInfoService
	.fetchTradingLimits()
	.asFlow()
	.collect { result ->
		// ...
	}
```