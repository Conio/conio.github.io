# User Signup

## Overview
---
`signup` API executes the signup process in Conio services. It allows client to create a new user and setting up a valid user session with passed username, password and crypto signature request.

## Parameters
---
The `SignupParams` used to initialize and perform `signup` API.

- credentials: the username and password used to execute the signup
- acceptances: the legal acceptances list accepted or not by the user during the signup
- crypto request: the crypto signature used to validate the signup

## Result
---
Success or error.

## Code
---
### iOS
```swift
let username: String = ...
let password: String = ...
let cryptoRequest = SignupParams
    .CryptoRequest
    .make(
        proofId: ...,
	    cryptoProof: ...,
	    proofExpiration: Timestamp(Date().timeIntervalSince1970 + (30 * 60 * 1000)),
	    username: username.,
	    userLevel: ...,
	    iban: ...,
	    email: ...,
	    firstName: ...,
	    lastName: ...
    )
let acceptences = [
    SignupParams.LegalAcceptance.makeAccepted(type: .clientSupport),
    SignupParams.LegalAcceptance.makeAccepted(type: .appImprovement)
]
let params = SignupParams
    .make(
        username: usernamem
        password: password:
        acceptances: acceptances,
        cryptoRequest: cryptoRequest
    )

userService
    .signup(with: params)
    .asPublisher()
    .sink { result in
        // ...
    }
```

### Android
```kotlin
val username: String = "..." // user unique identifier

val credentials = Credentials(
	username = username,
	password = "..."
)

val signupCryptoRequest = SignupCryptoRequest(
	cryptoProof = "...",
	proofId = "...",
	username = username,
	userLevel = "...",
	expiration = Date().time + (30 * 60 * 1000), // [example] 30 minutes from now
	iban = "...",
	email = "...",
	firstName = "...",
	lastName = "...",
)

val acceptances = listOf(
	Acceptance(AcceptanceType.AppImprovement, isAccepted = true),
	Acceptance(AcceptanceType.ClientSupport, isAccepted = true),
)

val signupParams = SignupParams(
  credentials = credentials,
  acceptances = acceptances,
  cryptoRequest = signupCryptoRequest
)

conio.userService
	.signup(params)
	.asFlow()
	.collect { result ->
		// ...
	}
```