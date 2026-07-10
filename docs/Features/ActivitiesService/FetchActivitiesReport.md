# Fetch Activities Report

## Overview

`fetchActivitiesReport` API is used to download an export of the Wallet activities over a time window as a PDF document.

## Params

The `FetchActivitiesReportParams` used to initialize and perform `fetchActivitiesReport` API.

- time frame: the time window of the activities to export. Timestamps are Unix time in milliseconds.

## Result

The `FetchActivitiesReportResult` containing the activities export.

- file data: the activities export in PDF format

## Code

### iOS
```swift
let params = FetchActivitiesReportParams.make(from: ..., to: ...)

activitiesService
    .fetchActivitiesReport(with: params)
    .asPublisher()
    .sink { result in
        if let report = try? result.get() {
            let pdf: Data = report.fileData
            // present / store the PDF
        }
    }
```

### Android
```kotlin
val params = FetchActivitiesReportParams(
    timeFrame = TimeFrame(fromTimeInMillis: ..., toTimeInMillis: ...)
)

conio.activityService
    .fetchActivitiesReport(params)
    .asFlow()
    .collect { result ->
        // ...
    }
```
