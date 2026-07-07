# Send Trading Report

## Overview

`sendTradingReport` API is used to send the trading financial report for a period to the Conio user via email. The available periods can be retrieved with [Get Available Trading Reports](./GetAvailableTradingReports.md).

## Params

The `SendTradingReportParams` used to initialize and perform `sendTradingReport` API.

- period: the `TradingReportPeriod` identifying the trading report by fiscal year and, optionally, a quarter (see [Get Available Trading Reports](./GetAvailableTradingReports.md))

## Result

Success or error.

## Code

### iOS
```swift
let params = SendTradingReportParams.make(
    period: TradingReportPeriod.make(year: "2025")
)

tradingInfoService
    .sendTradingReport(with: params)
    .asPublisher()
    .sink { result in
        switch result {
        case .success:
            // the report has been sent via email
            break
        case .failure(let error):
            // handle the error
            break
        }
    }
```

### Android
```kotlin
val params = SendTradingReportParams(
    period = TradingReportPeriod(year = "2025")
)

conio.tradingInfoService
    .sendTradingReport(params)
    .asFlow()
    .collect { result ->
        // the report has been sent via email
    }
```
