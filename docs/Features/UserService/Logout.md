# Logout

## Overview

`logout` API executes the user logout from Conio services invalidating user session.

## Result

### Success

No data

### Error

- One of [common errors](../Errors.md).

## Code

### iOS
```swift
userService
    .logout()
    .asPublisher()
    .sink { result in
        // ...
    }
```

### Android
```kotlin
conio.userService
	.logout()
	.asFlow()
	.collect { result ->
		// ...
	}
```