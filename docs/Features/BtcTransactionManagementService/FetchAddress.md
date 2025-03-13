# Fetch Address 

## Overview

`fetchAddress` API is used to retrieve the BTC wallet address. It allows client to fetch the BTC Wallet address and URI data.

## Result

The `BtcAddressResult` BTC wallet address data.

- address: the alphanumeric unique BTC wallet address
- uri: the Uniform Resource Identifier used to facilitate payments as per BIP-21

## Code

### iOS
```swift
btcTransactionManagementService
	.fetchAddress()
	.asPublisher
	.sink { result in 
		// ...
	}
```

### Android
```kotlin
conio.btcTransactionService
	.fetchAddress()
	.asFlow()
	.collect { result ->
		// ...
	}
```