# Android Configuration

The Conio Token SDK is divided into multiple services, each one providing a different set of APIs.

Each service is exposed by the `Conio` class that must be created with an Android `Context` and a `ConioConfiguration`.

The `ConioConfiguration` allow you to specify the execution environment of the Conio SDK and can be created with the url of the Conio Back-end.

```kotlin
val configuration = ConioConfiguration(
	// required
	baseUrl = "https://example.test.com"
	// optional
	// http headers added to each request, usefull for debug purpose
	headers = mapOf("header_key" to "header_value"),
)

val conio = Conio(configuration, context)
```

## Usage

### Consumer

The single Service API is initialized with its specific parameters (if necessary) and returns a `ServiceConsumer` that allow to choose how to launch the service:

- `.asCallback`: launch the service and notify the result calling the callback parameter;
- `.asFlow`: returns a [Flow](https://kotlinlang.org/api/kotlinx.coroutines/kotlinx-coroutines-core/kotlinx.coroutines.flow/-flow/) that will be launched once collected.

```kotlin
val serviceApi: ServiceConsumer<Success> = conio.userService.login(...)

// asFlow
serviceApi.asFlow().collect { result ->
	// ...
}
			
// asCallback
serviceApi.asCallback { result ->
	// ...        
}
```

### Result

No matter how you choose to launch the service, the service output is a `Result<S, ConioError>` instance, where the `S` generic type represent the data obtained in case of success and it depends on the service itself;

`Result` expose some properties and methods to access success data or failure reason.

```kotlin
val serviceApi: ServiceConsumer<Void> = conio.userService.login(...)

serviceApi.asFlow()
	.collect { result: Result<Success, ConioError> ->
		val value: Success? = result.value
		val error: ConioError? = result.error

		// or

		result.fold(
			onValue = { value: Success -> 
				... 
			},
			onError = { error: ConioError ->
				... 
			}
		)
	}
```