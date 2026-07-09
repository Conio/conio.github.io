# Accept New Legal Acceptances

## Overview

`acceptNewLegalAcceptances` API submits the user choices (accept or reject) for the legal acceptances. Each choice references the acceptance `id` obtained from [Fetch Legal Acceptances](./FetchLegalAcceptances.md). It allows client to mark new legal acceptances as accepted (or rejected) and let user continue operate on Conio services.

## Parameters

The `AcceptNewLegalAcceptancesParams` used to initialize and perform `acceptNewLegalAcceptances` API.

- username: the user username
- password: the user password
- legal acceptances: the `LegalAcceptancesParams` user choices for the legal acceptances

### LegalAcceptancesParams

The `LegalAcceptancesParams` containing the user choices. It can be built with the `make(userChoices:)` factory, or with the `makeAllAccepted(from:)` convenience factory that marks as accepted all the acceptances contained in a `LegalAcceptancesResult` fetched via `fetchLegalAcceptances`.

- user choices: the list of `LegalAcceptance` user choices

### LegalAcceptance

The `LegalAcceptance` single user choice. It can be built with the `makeAccepted(id:)` and `makeNotAccepted(id:)` factories.

- id: the acceptance identifier, provided by the backend
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
    username = "...",
    password = "...",
    legalAcceptances = LegalAcceptancesParams(
        userChoices = listOf(
            LegalAcceptance.makeAccepted(id = "..."),
            LegalAcceptance.makeNotAccepted(id = "..."),
        )
    ),
)

conio.userService
    .acceptNewLegalAcceptances(params)
    .asFlow()
    .collect { result ->
        // ...
    }
```
