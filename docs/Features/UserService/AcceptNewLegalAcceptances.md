# Accept New Legal Acceptances

## Overview

`acceptNewLegalAcceptances` API submits the user choices (accept or reject) for the legal acceptances. Each choice references the acceptance `id` obtained from [Fetch Legal Acceptances](./FetchLegalAcceptances.md). It allows client to mark new legal acceptances as accepted (or rejected) and let user continue operate on Conio services.

## Parameters

The `AcceptNewLegalAcceptancesParams` used to initialize and perform `acceptNewLegalAcceptances` API.

- credentials: the user username and password
- acceptances: the user choices for the legal acceptances

### LegalAcceptance

The `LegalAcceptance` single user choice.

- id: the acceptance identifier, obtained from [Fetch Legal Acceptances](./FetchLegalAcceptances.md)
- is accepted: the user choice, accepted (`true`) or rejected (`false`)

## Result

Success or error.

## Code

### iOS
```swift
let params = AcceptNewLegalAcceptancesParams.make(
    username: "...",
    password: "...",
    legalAcceptances: LegalAcceptancesParams.make(userChoices: [
        .makeAccepted(id: "..."),
        .makeNotAccepted(id: "...")
    ])
)

userService
    .acceptNewLegalAcceptances(with: params)
    .asPublisher()
    .sink { result in
        // ...
    }
```

### Android
```kotlin
val params = AcceptNewLegalAcceptancesParams(
    acceptances = listOf(
        LegalAcceptance(id = "...", isAccepted = true),
        LegalAcceptance(id = "...", isAccepted = false),
    ),
    credentials = Credentials(
        username = "...",
        password = "..."
    ),
)

conio.userService
    .acceptNewLegalAcceptances(params)
    .asFlow()
    .collect { result ->
        // ...
    }
```
