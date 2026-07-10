# Send Activities Report

## Overview

`sendActivitiesReport` API is used to send an export of the Wallet activities over a time window to the Conio user via email.

## Params

The `SendActivitiesReportParams` used to initialize and perform `sendActivitiesReport` API.

- time frame: the time window of the activities to export. Timestamps are Unix time in milliseconds.

## Result

Success or error.

## Code

### iOS
```swift
let params = SendActivitiesReportParams.make(from: ..., to: ...)

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
val params = SendActivitiesReportParams(
    timeFrame = TimeFrame(fromTimeInMillis: ..., toTimeInMillis: ...)
)

conio.activityService
    .sendActivitiesReport(params)
    .asFlow()
    .collect { result ->
        // check the result: success or error
    }
```
