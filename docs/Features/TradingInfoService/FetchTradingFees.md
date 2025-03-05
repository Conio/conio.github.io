# Fetch Trading Fees

## Overview

`fetchTradingFees` API is used to retrieve the trading fees linked to Conio user. It allows client to fetch the trading fees involved in the Conio user trading operations.

## Result

The `TradingFeesResult` trading fees involved in the Conio user trading operations.

- buy service fees: the buy trading fees list
- sell service fees: the sell trading fees list
- swap service fees: the swap trading fees list
- transfer service fees: the transfer trading fees list

## Code

### iOS
```swift
tradingInfoService
	.fetchTradingFees()
	.asPublisher()
	.sink { result in 
		...
	}
```


### Android
```kotlin
conio.tradingInfoService
	.fetchTradingFees()
	.asFlow()
	.collect { result ->
		// ...
	}
```