# Get User Tc

## Overview

`getUserTc` API fetches the current acceptance state of the user's legal acceptances (terms & conditions, privacy policy and other informative). For each acceptance it returns its status and the optional acceptance timestamp. Use the acceptance `id` to correlate each state with the document details returned by [Fetch Legal Acceptances](./FetchLegalAcceptances.md). It requires an authenticated user session.

## Params

None.

## Result

The `UserTcResult` containing the user acceptance states.

- acceptances: the list of acceptance states

### Acceptance

The `UserTcResult.Acceptance` acceptance state.

- id: the acceptance identifier, provided by the backend
- status: the current acceptance status
- accepted at: the acceptance epoch timestamp, when available

### Status

The `UserTcResult.Status` acceptance status.

- to accept: the acceptance is still to be accepted by the user
- accepted: the acceptance has been accepted by the user
- rejected: the acceptance has been rejected by the user

## Code

### iOS
```swift
userService
    .getUserTc()
    .asPublisher()
    .sink { result in
        // use result.get().acceptances
    }
```

### Android
```kotlin
conio.userService
    .getUserTc()
    .asFlow()
    .collect { result ->
        // ...
    }
```
