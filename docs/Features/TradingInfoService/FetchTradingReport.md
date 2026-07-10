# Fetch Trading Report

## Overview

`fetchTradingReport` API is used to retrieve the trading financial report linked to Conio user as a PDF document. It allows client to specify the trading report period as a fiscal year and, optionally, a quarter. The available periods can be retrieved with [Get Available Trading Reports](./GetAvailableTradingReports.md).

## Parameters

The `FetchTradingReportParams` used to initialize and perform `fetchTradingReport` API.

- period: the `TradingReportPeriod` identifying the trading report by fiscal year and, optionally, a quarter (see [Get Available Trading Reports](./GetAvailableTradingReports.md))

## Result

The `TradingReportResult` trading report info involved in the Conio user trading operations.

- pdf: the trading report in PDF format

## Code

### iOS
```swift
let params = FetchTradingReportParams.make(
    period: TradingReportPeriod.make(year: "2025", quarter: .q1)
)

tradingInfoService
    .fetchTradingReport(with: params)
    .asPublisher()
    .sink { result in
        if let report = try? result.get() {
            let pdf: Data = report.pdf
            // present / store the PDF
        }
    }
```

### Android
```kotlin
val params = FetchTradingReportParams(
    period = TradingReportPeriod(year = "2025", quarter = TradingReportPeriod.Quarter.Q1)
)

conio.tradingInfoService
    .fetchTradingReport(params)
    .asFlow()
    .collect { result ->
        // ...
    }
```
