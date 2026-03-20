# Create Wallet Address

## Overview

`createWalletAddress` API creates a new wallet address associated with an existing `AddressBookEntry`.

## Params

The `CreateAddressBookWalletAddressParams` used to initialize and perform `createWalletAddress` API.

- address book id: id referencing the parent `AddressBookEntry`.
- wallet address: wallet address details to create.

## Result

The `CreateAddressBookWalletAddressResult` contains the complete `AddressBookWalletAddress` with id's.

- wallet address: the newly created wallet address with full details.

## Code

### iOS
```swift
let params = CreateAddressBookWalletAddressParams.make(
    addressBookId: ...,
    CreateAddressBookWalletAddress.make(
        walletAddress: ...,
        isForeign: ...,
        isUnhostedWallet: ...,
        vase: ...,
        proofOfOwnership: ...,
        label: ...,
        threshold: ...
    )
)

addressBookService
    .createWalletAddress(params: params)
    .asPublisher()
    .sink { result in
        // ...
    }
```

### Android
```kotlin
val vasp = Vasp(
    name = "...",
    did = "...",
    websiteUrl = "..."
)

val proofOfOwnership = ProofOfOwnership(
    message = ProofOfOwnershipMessage(
        value = "..."
    ),
    signature = ProofOfOwnershipSignature(
        value = "..."
    )
)

val walletAddress = CreateAddressBookWalletAddress(
    walletAddress = "...",
    isForeign = "...",
    isUnhostedWallet = "...",
    vasp = vasp,
    proofOfOwnership = proofOfOwnership,
    label = "...",
    threshold = FiatAmount()
)

val params = CreateAddressBookWalletAddressParams(
    addressBookId = "...",
    walletAddress = walletAddress
)

conio.addressBookService
    .createWalletAddress(params)
    .asFlow()
    .collect { result -> 
        //...
    }
```