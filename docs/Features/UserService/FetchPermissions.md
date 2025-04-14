# Fetch User Permissions

## Overview

`fetchPermissions` API is used to retrieve the service permissions list the user can currently use.

## Result

The `PermissionsResult` contains the `PermissionType` list. If a service permission is not on the list means that the related service can not be completed without an error.

- types: the available permission types list

## Code

### iOS
```swift
userService
	.fetchPermissions()
	.asPublisher()
	.sink { result in 
		...
	}
```

### Android
```kotlin
conio.userService
	.fetchPermissions()
	.asFlow()
	.collect { result ->
		
	}
```