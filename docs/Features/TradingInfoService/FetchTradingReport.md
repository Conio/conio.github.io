# Fetch Trading Report

## Overview

`fetchTradingReport` API is used to retrieve the trading financial report linked to Conio user. It allows client to either specify the exact year or the last year trading effective time to fetch the trading report involved in the Conio user trading operations.

## Parameters

The `FetchTradingReportParams` used to initialized and perform `fetchTradingReport` API.

- period: the trading report period of time either as exact year or last year

## Result

The `TradingReportResult` trading report info involved in the Conio user trading operations.

- pdf: the trading report in PDF format

## Code

### iOS
```swift
let params = FetchTradingReportParams.make(period: .lastYear)

tradingInfoService
	.fetchTradingReport(with: params)
	.asPublisher()
	.sink { result in 
		...
	}
```

### Android
```kotlin
// val reportPeriod = FetchTradingReportParams.ReportPeriod.LastYear
val reportPeriod = FetchTradingReportParams.ReportPeriod("2023")

val params = FetchTradingReportParams(
	period = reportPeriod
)

conio.tradingInfoService
	.fetchTradingReport(params)
	.asFlow()
	.collect { result ->
		// ...
	}
```