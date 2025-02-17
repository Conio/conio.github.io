# Change password

## Overview

`changePassword` API executes a user change password. Allows the client to change the password of the authenticated user.

## Context

**Authentication**: required

## Parameters

The `ChangePasswordParams` used to initialized and perform `changePassword` API.

- old password: the current user password, needed to approve the change password request
- new password: the new user password

## Result

### Success

No data

### Error

- `Unauthorized`: the old password provided is wrong or there is no valid session
- One of [common errors](../Errors.md)

## Code

### iOS

```swift
let params = ChangePasswordParams(
	oldPassword: ...,
	newPassword: ...
)

conio.userService
	.changePassword(with: params)
	.asPublisher()
	.sink { result in
		// ...
	}
```

### Android

```kotlin

val params = ChangePasswordParams(
	oldPassword: ...,
	newPassword: ...
)

conio.userService
	.changePassword(params)
	.asFlow()
	.collect { result ->
		// ...
	}
```