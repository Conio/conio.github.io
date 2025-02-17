# Login

## Overview

`login` API executes the login in Conio services. Allows the client to obtain a valid user session by passing a username and password.

## Parameters

The `LoginParams` used to initialized and perform `login` API.

- username: the username used to execute the login
- password: the user password used to execute the login

## Result

### Success

No data

### Error

- `Unauthorized`: the credentials provided are wrong
- One of [common errors](../Errors.md)

## Code

### iOS

```swift
let credentials = Credentials(
	username: ...,
	password: ...
)

let params = LoginParams(
	credentials: credentials
)
	
conio.userService
	.login(with: params)
	.asPublisher()
	.sink { result in
		// ...
	}
```

### Android

```kotlin
val credentials = Credentials(
	username = ...,
	password = ...
)

val params = LoginParams(
	credentials = credentials
)

conio.userService
	.login(params)
	.asFlow()
	.collect { result ->
		// ...
	}
```