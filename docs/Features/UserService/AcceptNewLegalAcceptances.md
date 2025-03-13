# Accept New Legal Acceptances

## Overview

`acceptNewLegalAcceptances` API is used to mark as accepted the new legal acceptances. It allows client to mark as accepted possible new legal acceptances and let user continue operate on Conio services.

## Parameters

The `AcceptNewLegalAcceptancesParams` used to initialized and perform `acceptNewLegalAcceptances` API.

- credentials: the username and password used to execute the signup
- acceptances: the new legal acceptances user preferences

## Result

### Success

No data

### Error

- `Unauthorized`: the credentials provided are wrong or the user is not authorized to execute the service.
- `ClientSupportAcceptanceNotAccepted`: the required acceptance `ClientSupport` was refused.
- `AppImprovementAcceptanceNotAccepted`: the required acceptance `AppImprovement` was refused.
- One of [common errors](../Errors.md).

## Code

### iOS
```swift
let acceptences = LegalAcceptancesParams.makeAllAccepted()
let params = AcceptNewLegalAcceptancesParams
    .make(
        username: ...,
        password: ...,
        legalAcceptances: acceptances
    )
userService
	.acceptNewLegalAcceptances(with: params)
	.asPublisher()
	.sink { result in 
		...
	}
```

### Android
```kotlin
val acceptances = listOf(
    Acceptance(AcceptanceType.AppImprovement, isAccepted = true),
    Acceptance(AcceptanceType.ClientSupport, isAccepted = true),
)

val credentials = Credentials(
    username = "..." // user unique identifier,
    password = "..."
)

val params = AcceptNewLegalAcceptancesParams(
    acceptances = B2BModelAcceptances.acceptedAcceptances,
    credentials = credentials
)

conio.userService
    .acceptNewLegalAcceptances(params)
    .asFlow()
    .collect { result ->
        // ...
    }
```