# Fetch Balances

## Overview

`fetchBalances` API is used to retrieve the wallet balances of all cryptocurrencies. It allows client to fetch the Wallets balances amounts, either confirmed and unconfirmed.

## Result

### Success

The `BalancesResult` contains the `WalletBalance` list.

Each `WalletBalance` contains:

- crypto currency: the crypto currency related to the balance.
- confirmed balance: the balance amount confirmed by the blockchain or by Conio (in case of Conio2Conio transaction).
- unconfirmed balance: the balance amount the blockchain still need to confirm.

### Error

- One of [common errors](../Errors.md).

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