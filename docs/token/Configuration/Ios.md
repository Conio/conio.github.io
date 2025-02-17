# iOS Configuration

The Conio Token SDK is divided into multiple services, each one providing a different set of APIs.

Each service is exposed by the `Conio` class and to obtain a `Conio` instance, you must first call the `Conio.setup` static method with a `ConioConfiguration`, followed by calling the `Conio.instance` static method.

The `ConioConfiguration` allow you to specify the execution environment of the Conio SDK and can be created with the url of the Conio Back-end.

```swift
let configuration = ConioConfiguration(
	baseUrl: "https://example.test.com"
)

try! Conio.setup(serviceConfiguration: configuration)

let conio = try! Conio.instance()
```

!!! warning
	The `Conio.setup` static method cannot be called more than once.

## Usage

### Consumer

The single `Service` API is initialized with its specific parameters (if necessary) and returns a `ServiceConsumer` that allow to choose how to launch the service:

- `.asCallback`: launch the service and notify the result calling the callback parameter;
- `.asPublisher`: launch the service and returns a [Combine Publisher](https://developer.apple.com/documentation/combine/anypublisher/)
- `.run`: only launch the service (complete silently).

```swift
let serviceApi: ServiceConsumer<Void> = conio.userService.login(...)

// asPublisher
let cancellable = serviceApi.asPublisher().sink { result in 
	// ...
}
			
// asCallback
serviceApi.asCallback { result in
	// ...        
}

// run
serviceApi.run()  
```

### Result

No matter how you choose to launch the service, the service output is a [Swift Result](https://developer.apple.com/documentation/swift/result) where:

- the `Success` associated value depends on the service itself
- the `Failure` associated value is a `ConioError`

```swift
let serviceApi: ServiceConsumer<Void> = conio.userService.login(...)

serviceApi.asPublisher()
	.sink { result in // Result<Void, ConioError>
		switch result {
		case .success:
			// ...
		case .failure(let error): // ConioError
			// ...
		}
	}
```