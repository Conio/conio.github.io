# Fetch Balances

## Overview

`fetchBalances` API is used to retrieve the wallet balances of all cryptocurrencies. It allows client to fetch the Wallets balances amounts, either confirmed and unconfirmed.

## Result

The `BalancesResult` contains the `WalletBalance` list.

- wallets balances: the available wallets balances list

## Code

### iOS
```swift
userService
	.fetchBalances()
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