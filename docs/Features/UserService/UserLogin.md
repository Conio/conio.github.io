# User Login

## Overview
---
`login` API executes the login in Conio services. It allows client to obtain a valid user session with passed username, password and crypto signature request.

## Parameters
---
The `LoginParams` used to initialized and perform `login` API.

- username: the username used to execute the login
- password: the user password used to execute the login
- crypto request: the crypto signature used to validate the login

## Result
---
Success or error.

## Code
---
### iOS
```swift
let username: String = ...
let password: String = ...
let cryptoRequest = LoginParams
    .CryptoRequest
    .make(
        username: username,
        expiration: Timestamp(Date().timeIntervalSince1970 + (30 * 60 * 1000)),
        cryptoProof: ...
    )
    
userService
    .login(with: params)
    .asPublisher()
    .sink { result in
        // ...
    }
```

### Android
```kotlin
val username: String = ...
val credentials = Credentials(
	username = username,
	password = ...
)

val loginCryptoRequest = LoginCryptoRequest(
	cryptoProof = "...",
	username = username,
	expiration = Date().time + (30 * 60 * 1000)
)

val loginParams = LoginParams(
  credentials = credentials,
  cryptoRequest = loginCryptoRequest
)

conio.userService
	.login(params)
	.asFlow()
	.collect { result ->
		// ...
	}
```