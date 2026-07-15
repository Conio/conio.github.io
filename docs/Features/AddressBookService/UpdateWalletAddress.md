# Update Wallet Address

## Overview

`updateWalletAddress` API updates the label of a wallet address within an address book entry. Only the label can be modified: all the other wallet address fields remain unchanged.

## Params

The `UpdateWalletAddressParams` used to initialize and perform `updateWalletAddress` API.

- address book id: the unique identifier of the address book entry that contains the wallet address
- wallet address id: the unique identifier of the wallet address to update
- label: the new label for the wallet address

## Result

The `UpdateWalletAddressResult` containing the updated wallet address.

- updated wallet address: the updated wallet address

### Errors

List of the possible errors that can be returned by this API:

- `AddressBookNotFound`: Address Book entry specified wasn't found
- `WalletAddressNotFound`: Address Book Wallet Address entry specified wasn't found

## Code

### iOS
```swift
let params = UpdateWalletAddressParams.make(
    addressBookId: "...",
    walletAddressId: "...",
    label: "..."
)

addressBookService
    .updateWalletAddress(params: params)
    .asPublisher()
    .sink { result in
        // ...
    }
```

### Android
```kotlin
val params = UpdateWalletAddressParams(
    addressBookId = "...",
    walletAddressId = "...",
    label = "..."
)

conio.addressBookService
    .updateWalletAddress(params)
    .asFlow()
    .collect { result ->
        // ...
    }
```
