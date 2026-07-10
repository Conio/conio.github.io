# Get Available Trading Reports

## Overview

`getAvailableTradingReports` API is used to retrieve the list of trading report periods available for the Conio user. It allows client to know which fiscal years and quarters can be used to fetch or send a trading report.

## Params

None.

## Result

The `AvailableTradingReportsResult` containing the available trading report periods.

- report periods: the list of `TradingReportPeriod` available for the Conio user

### TradingReportPeriod

The `TradingReportPeriod` identifies a trading report by fiscal year and, optionally, a quarter.

- year: the fiscal year (e.g. "2025"). If not provided, it identifies the previous fiscal year
- quarter: the optional quarter of the fiscal year (`q1`, `q2`, `q3`, `q4`). If not provided, it identifies the whole year

## Code

### iOS
```swift
tradingInfoService
    .getAvailableTradingReports()
    .asPublisher()
    .sink { result in
        // use result.get().reportPeriods
    }
```

### Android
```kotlin
conio.tradingInfoService
    .getAvailableTradingReports()
    .asFlow()
    .collect { result ->
        // ...
    }
```
