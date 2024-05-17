# User Logout

## Overview
---
`logout` API executes the user logout from Conio services invalidating user session.

## Result
---
Success or error.

## Code
---
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