# iOS Configuration

`ConioB2BSDK` is divided into multiple services, each one providing a different set of APIs.<br>

Each service is independent and can be initialized through a `ServiceConfiguration` configuration using its own factory.
```swift
let conioConfig = ConioConfiguration.makeTestConfiguration(baseUrl: ...)
let userService = UserServiceFactory().makeServiceUsingConfiguration(conioConfig)

// User Service ready to be used
userService
    .login(with: ...)
    .asPublisher()
    .sink { ... }
// ...  
```

Otherwise, `ConioB2BServiceFactory` factory leverages on a single `ServiceFactory` to make the requested `Service`.
```swift
let conioConfig = ConioConfiguration.makeTestConfiguration(baseUrl: ...)
let userService = ConioB2BServiceFactory.makeServiceUsingFactory(UserServiceFactory(), serviceConfiguration: conioConfig)
let walletService = ConioB2BServiceFactory.makeServiceUsingFactory(WalletServiceFactory(), serviceConfiguration: conioConfig)
let activitiesService = ConioB2BServiceFactory.makeServiceUsingFactory(ActivitiesServiceFactory(), serviceConfiguration: conioConfig)
// ...  
```

## Usage
The single `Service` API is initialized with its specific `Params` parameters (if necessary) and the output can be read through its `OperationResult` result.
```swift
// ...
let params = LoginParams
    .make(
        username: ...,
        password: ...,
        cryptoRequest: ...
    )

userService
    .login(with: params)
    .asPublisher()
    .sink { result in
        switch result {
        case .success:
            // ...
        case .failure(let error):
            // ...
        }
    }
    .store(in: ...)
// ...  
```

Each API is returned as `ServiceConsumer` and can be consumed in three different ways:

* `asPublisher()`, used to handle the result in a declarative way leveraging on [Combine](https://developer.apple.com/documentation/combine);
* `asCallback()`, used to handle the result in closure/lambda style as self-contained block;
* `run()`, used to execute the API without handling the result.

```swift
// asPublisher()
let cancellable = userService
    .logout()
    .asPublisher()
    .sink { result in 
        // ...
    }
            
// asCallback()
userService
    logout()
    .asCallback { result in
        // ...        
    }

// run()
userService
    .logout()
    .run()  
```
