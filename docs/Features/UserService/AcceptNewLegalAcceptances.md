# Accept New Legal Acceptances

## Overview
---
`acceptNewLegalAcceptances` API is used to mark as accepted the new legal acceptances. It allows client to mark as accepted possible new legal acceptances and let user continue operate on Conio services.

## Parameters
---
The `AcceptNewLegalAcceptancesParams` used to initialized and perform `acceptNewLegalAcceptances` API.

- credentials: the username and password used to execute the signup
- acceptances: the new legal acceptances user preferences

## Result
---
Success or error.

## Code
---
### iOS
```swift
let acceptences = [
    SignupParams.LegalAcceptance.makeAccepted(type: .clientSupport),
    SignupParams.LegalAcceptance.makeAccepted(type: .appImprovement)
]
let params = AcceptNewLegalAcceptancesParams
    .make(
        username: ...,
        password: ...,
        legalAcceptances: acceptances
    )
luserService
	.acceptNewLegalAcceptances(with: params)
	.asPublisher()
	.sink { result in 
		...
	}
```

### Android
(TBD)