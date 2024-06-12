# Fetch Activity 

## Overview
---
`fetchActivity` API fetches a specific Wallet activity. It allows client to specify an activity identifier to query and retrieve the related activity.

## Params
---
The `FetchActivityParams` used to initialize and perform `fetchActivity` API.

- activity id: the activity unique identifier

## Result
---
The `ActivityResult` contains.

- activity: the Wallet activity related to the identifier specified in params

## Code
---
### iOS
```swift
let params = FetchActivityParams.make(activityId: ...)
    
    activitiesService
    .fetchActivities(with: params)
    .asPublisher()
    .sink { result in
        // ...
    }
```

### Android
```kotlin
(TBD)
```