# Create Wallet Address

## Overview

`createWalletAddress` API creates a new wallet address associated with an existing `AddressBookEntry`.

## Params

The `CreateAddressBookWalletAddressParams` used to initialize and perform `createWalletAddress` API.

- address book id: id referencing the parent `AddressBookEntry`.
- wallet address: wallet address details to create. For more informations check [`CreateAddressBookWalletAddress` definition](./CreateAddressBookEntryWithWalletAddress.md#createaddressbookwalletaddress).

## Result

The `CreateAddressBookWalletAddressResult` contains the complete `AddressBookWalletAddress` with id's.

- wallet address: the newly created wallet address with full details.

### Errors

List of the possible errors that can be returned by this API:

- `AddressBookNotFound`: Address Book entry specified wasn't found
- `AddressAlreadyUsed`: Wallet Address already present in one Address Book entry
- `WalletAddressInvalidParameters`: invalid parameters provided to create an Address Book Wallet Address entry
- `WalletAddressValidationError`: unable to create/update an Address Book Wallet Address because the provided parameters are not conformed to the Travel Rule / Agenzia delle Entrate requirements

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
// val vasp = Vasp.buildWithDid(
//      name = "...",
//      did = "..."
//  )
val vasp = Vasp.buildWithWebsite(
    name = "...",
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
    isForeign = false,
    isUnhostedWallet = false,
    vasp = vasp,
    proofOfOwnership = proofOfOwnership,
    label = "...",
    threshold = FiatAmount(1000)
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