# Delete Wallet Address

## Overview

`deleteWalletAddress` API deletes a single wallet address from an address book entry. The address book entry itself is not deleted: to remove the whole entry use [Delete Address Book Entry](./DeleteAddressBookEntry.md).

## Params

The `DeleteWalletAddressParams` used to initialize and perform `deleteWalletAddress` API.

- address book id: the unique identifier of the address book entry that contains the wallet address
- wallet address id: the unique identifier of the wallet address to delete

## Result

The `DeleteWalletAddressResult` containing the deleted wallet address.

- deleted wallet address: the deleted wallet address

## Code

### iOS
```swift
let params = DeleteWalletAddressParams.make(
    addressBookId: "...",
    walletAddressId: "..."
)

addressBookService
    .deleteWalletAddress(params: params)
    .asPublisher()
    .sink { result in
        // ...
    }
```

### Android
```kotlin
val params = DeleteWalletAddressParams(
    addressBookId = "...",
    walletAddressId = "..."
)

conio.addressBookService
    .deleteWalletAddress(params)
    .asFlow()
    .collect { result ->
        // ...
    }
```
