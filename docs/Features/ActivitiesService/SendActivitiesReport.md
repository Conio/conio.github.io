# Send Activities Report

## Overview

`sendActivitiesReport` API is used to send an export of the Wallet activities over a time window to the Conio user via email.

## Params

The `SendActivitiesReportParams` used to initialize and perform `sendActivitiesReport` API.

- time frame: the `TimeFrameParams` time window of the activities to export. Timestamps are Unix time in milliseconds. // iOS: Int64, Android: Long

## Result

Success or error.

## Code

### iOS
```swift
let params = FetchActivitiesReportParams.make(from: ..., to: ...)

activitiesService
    .sendActivitiesReport(with: params)
    .asPublisher()
    .sink { result in
        switch result {
        case .success:
            // the export has been sent via email
            break
        case .failure(let error):
            // handle the error
            break
        }
    }
```

### Android
```kotlin
val params = FetchActivitiesReportParams(
    timeFrame = TimeFrame(fromTimeInMillis: ..., toTimeInMillis: ...)
)

conio.activityService
    .sendActivitiesReport(params)
    .asFlow()
    .collect { result ->
        // the export has been sent via email
    }
```
