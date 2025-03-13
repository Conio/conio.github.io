# Fetch Mnemonic

## Overview

`fetchMnemonic` API is used to retrieve the user wallet mnemonic, a list of secret words necessary to restore user wallet during account recovery.

## Result

The `MnemonicResult` contains the list of words that represent the user wallet mnemonic.

- words: the mnemonic words list

## Code

### iOS
```swift
walletService
	.fetchMnemonic()
	.asPublisher()
	.sink { result in 
		...
	}
```

### Android
```kotlin
conio.walletService
	.fetchBalances()
	.asFlow()
	.collect { result ->
		// ...
	}
```