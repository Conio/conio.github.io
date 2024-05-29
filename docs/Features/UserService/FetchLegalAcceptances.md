# Fetch Legal Acceptances

## Overview
---
`fetchLegalAcceptances` API fetches the acceptances, terms and conditions and privacy policies information.

## Parameters
---
The `FetchLegalAcceptancesParams` used to initialized and perform `fetchLegalAcceptances` API.

- language: the legal acceptances language translation

## Result
---
The `LegalAcceptancesResult` acceptances, terms and conditions and privacy policies information.

- terms and conditions url: the T&C url
- privacy policies url: the privacy policies url
- acceptances: the acceptances list

## Code
---
### iOS
```swift
let params = FetchLegalAcceptancesParams.makeItalian()

userService
	.fetchLegalAcceptances(with: params)
	.asPublisher()
	.sink { result in 
		...
	}
```

### Android
```kotlin
val params = FetchLegalAcceptancesParams(
	language = Language.English,
)

conio.userService
	.fetchLegalAcceptances(params)
	.asFlow()
	.collect { result ->
		// ...
	}
```