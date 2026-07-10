# Associate Sender Info To Receive

## Overview

`associateSenderInfoToReceive` API associates the sender of a receive — an address book contact with one of its wallet addresses — to the receive itself. It provides the sender information required by the Travel Rule validation process for receives in the `waitingForValidationData` status.

The typical flow is:

1. **Detect a receive waiting for sender data.** Fetch the activities: a `ReceiveActivity` whose `validationStatus` is `waitingForValidationData` requires the sender information. Keep its `receiveId`.
2. **Create the sender contact.** Create a new address book entry with the sender's wallet address (see [Create Address Book Entry With Wallet Address](./CreateAddressBookEntryWithWalletAddress.md)), with `isVisible: false` so it does not appear in the user's address book list.
3. **Associate the sender to the receive.** Call `associateSenderInfoToReceive` with the `receiveId`, the `addressBookId` and the `walletAddressId`.
4. **Track the validation.** After the association the receive goes through the Conio validation process (`waitingForValidation`), which can end with the received amount being credited (`confirmed`) or with the sender data being rejected (`validationFailed`). The updated status may not be visible immediately when re-fetching the activity.

## Params

The `AssociateSenderInfoToReceiveParams` used to initialize and perform `associateSenderInfoToReceive` API.

- receive id: the unique identifier of the receive operation (from `ReceiveActivity.receiveId`)
- address book id: the unique identifier of the sender in the address book
- wallet address id: the unique identifier of the wallet address associated with the sender

## Result

Success or error.

## Code

### iOS
```swift
let params = AssociateSenderInfoToReceiveParams.make(
    receiveId: receiveId,
    addressBookId: addressBookId,
    walletAddressId: walletAddressId
)

addressBookService
    .associateSenderInfoToReceive(with: params)
    .asPublisher()
    .sink { result in
        // on success, re-fetch the activity to observe the updated status
    }
```

### Android
```kotlin
val params = AssociateSenderInfoToReceiveParams(
    receiveId = "...",
    addressBookId = "...",
    walletAddressId = "..."
)

conio.addressBookService
    .associateSenderInfoToReceive(params)
    .asFlow()
    .collect { result ->
        // on success, re-fetch the activity to observe the updated status
    }
```
