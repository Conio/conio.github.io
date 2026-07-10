# Fetch Legal Acceptances

## Overview

`fetchLegalAcceptances` API fetches the list of legal acceptances (terms & conditions, privacy policy and other informative) to present to the user. The content is returned already localized for the requested language.

Acceptances are id-based: each acceptance is identified by an opaque `id` provided by the backend. The same `id` is the key that correlates the document details with the user acceptance state ([Get User Tc](./GetUserTc.md)) and with the user choices ([Accept New Legal Acceptances](./AcceptNewLegalAcceptances.md)).

## Parameters

The `FetchLegalAcceptancesParams` used to initialize and perform `fetchLegalAcceptances` API.

- language: the legal acceptances language translation

## Result

The `LegalAcceptancesResult` containing the legal acceptances to present.

- acceptances: the acceptances list

### Acceptance

The `LegalAcceptancesResult.Acceptance` legal acceptance details.

- id: the acceptance identifier, provided by the backend
- title: the acceptance title
- body: the acceptance body text, when available
- url: the acceptance document url, when available
- is mandatory: indicates whether the acceptance is mandatory

## Code

### iOS
```swift
let params = FetchLegalAcceptancesParams.makeItalian()

userService
    .fetchLegalAcceptances(with: params)
    .asPublisher()
    .sink { result in
        // use result.get().acceptances
    }
```

### Android
```kotlin
val params = FetchLegalAcceptancesParams(
    language = Language.Italian,
)

conio.userService
    .fetchLegalAcceptances(params)
    .asFlow()
    .collect { result ->
        // ...
    }
```
