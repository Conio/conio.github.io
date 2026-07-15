# Delete Address Book Entry

## Overview

`deleteAddressBookEntry` API deletes an address book entry, together with its associated wallet addresses. To delete a single wallet address without removing the entry use [Delete Wallet Address](./DeleteWalletAddress.md).

## Params

The `DeleteAddressBookEntryParams` used to initialize and perform `deleteAddressBookEntry` API.

- address book id: the unique identifier of the address book entry to delete

## Result

The `DeleteAddressBookEntryResult` containing the deleted address book entry.

- deleted entry: the deleted address book entry

### Errors

List of the possible errors that can be returned by this API:

- `AddressBookNotFound`: Address Book entry specified wasn't found

## Code

### iOS
```swift
let params = DeleteAddressBookEntryParams.make(
    addressBookId: "..."
)

addressBookService
    .deleteAddressBookEntry(params: params)
    .asPublisher()
    .sink { result in
        // ...
    }
```

### Android
```kotlin
val params = DeleteAddressBookEntryParams(
    addressBookId = "..."
)

conio.addressBookService
    .deleteAddressBookEntry(params)
    .asFlow()
    .collect { result ->
        // ...
    }
```
