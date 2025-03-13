# Login

## Overview

`login` API executes the login in Conio services. It allows client to obtain a valid user session with passed username, password and crypto signature request.

## Parameters

The `LoginParams` used to initialized and perform `login` API.

- username: the username used to execute the login
- password: the user password used to execute the login
- crypto request: the crypto signature used to validate the login. The [plain message (`DATA_TO_SIGN`)](../CryptoRequest.md) to be signed in order to generate the crypto proof must adhere to the following format:

```
<external_user_id>|LOGIN|<proof_expiration>
```

## Result

### Success

No data

### Error

- `Unauthorized`: the credentials provided are wrong.
- `AcceptTC`: the user need to [accept the new T&C and Privacy Policy](./AcceptNewLegalAcceptances.md).
    - on Android: `ConioException.Unauthorized` with `forCurrentScope = SessionScope.AcceptTC`
- `InvalidCryptoProof`: the crypto proof sent is wrong ([check the cause](../CryptoRequest.md#error)).
- One of [common errors](../Errors.md).

## Code

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