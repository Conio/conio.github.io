# Fetch Activities

## Overview

`fetchActivities` API is used to retrieve the paginated list of Wallet activities. It allows client to filter activity by cryptocurrency, the type of activities and timeframe.

## Params

The `FetchActivitiesParams` used to initialize and perform `fetchActivities` API.

- crypto id: filter to retrieve only activities of a specific crypto currency
- activities types: filter to retrieve only specific activities types
- time frame: filter to retrieve activities created in a specific time frame
- pagination limit: the maximum activities number to fetch
- page: identifier of a specific activity page

## Result

The `ActivitiesResult` contains the list of activities and an identifier to fetch the next page.

- activities: the Wallet activities matching the information specified in params
- next page: the identifier of the next activities page, that can be used to call again `fetchActivities` with the same filters to retrive more activities.

## Code

### iOS
```swift
let params = FetchActivitiesParams
    .makeUsingAllActivityTypes(
        cryptoId: "cETH",
        timeFrame: .makeUsingLasYear(),
        paginationLimit: 6
    )

activitiesService
    .fetchActivities(with: params)
    .asPublisher()
    .sink { result in
        // ...
    }
```

### Android
```kotlin
import kotlin.time.Duration.Companion.days

val params = FetchActivitiesParams(
    cryptoId = "cETH",
    timeFrame = TimeFrame(
        fromTimeInMillis = TimeFrame.now() - 365.days.inWholeMilliseconds
    ),
    paginationLimit = 6
)

conio.activityService
    .fetchActivities(params)
    .asFlow()
    .collect {
        // ...
    }
```