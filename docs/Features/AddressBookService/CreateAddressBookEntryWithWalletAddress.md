# Create Address Book Entry With Wallet Address

## Overview

`createAddressBookEntryWithWalletAddress` API is used to create a new address book contact together with its first wallet address. It allows client to create both the contact and the wallet address atomically in a single API call.

## Params

The `CreateAddressBookEntryWithWalletAddressParams` used to initialized and perform `createAddressBookEntryWithWalletAddress` API.

- address book: the `CreateAddressBookEntry` contact details
- wallet address: the `CreateAddressBookWalletAddress` initial wallet address to associate with the contact

### CreateAddressBookEntry

The `CreateAddressBookEntry` contact creation data.

- first name: the contact first name
- last name: the contact last name
- label: the custom label or nickname for the contact
- is wallet owner: indicates whether the new address book entry belongs to the current user
- residence address: the optional residential or primary address information
- company info: the optional company information, if the contact represents a business entity
- person info: the optional personal information, if the contact represents an individual
- is visible: optionally indicates whether the entry should be shown in the address book list. If not provided, the entry will be visible by default. Creating a hidden entry is useful when a contact is created on the fly as part of another flow — for example the sender of a receive (see [Associate Sender Info To Receive](./AssociateSenderInfoToReceive.md)). Note that the visibility flag is currently write-only: the address book entry model returned by the read APIs does not include it

### CreateAddressBookWalletAddress

The `CreateAddressBookWalletAddress` wallet address creation data.

- wallet address: the actual blockchain wallet address
- is foreign: indicates whether the wallet should be considered foreign. It should be `true` if either the VASP associated with the wallet is located abroad or the wallet owner resides abroad
- is unhosted wallet: indicates whether this is an unhosted (self-custodied) wallet, meaning it is not managed by a VASP
- vasp: the optional `Vasp` associated with the wallet. It must not be provided if the wallet is unhosted
- proof of ownership: the optional `ProofOfOwnership` for the wallet address. It must be provided only if the wallet is unhosted, the contact is the wallet owner and the threshold is null (no limits) or greater than or equal to 1000 EUR
- label: the optional custom label for the wallet address
- threshold: the fiat threshold amount for a single send transaction, associated to the new wallet address entry. Set to null for no limits. 

## Result

The `CreateAddressBookEntryWithWalletAddressResult` created address book data.

- entry: the complete `FullAddressBookEntry` with the generated identifiers and the associated wallet addresses

### Errors

List of the possible errors that can be returned by this API:

- `DuplicatedNickname`: unable to create/update an Address Book entry because the provided label is already used for another entry
- `AddressAlreadyUsed`: Wallet Address already present in one Address Book entry
- `AddressBookInvalidParameters`: invalid parameters provided to create an Address Book entry
- `WalletAddressInvalidParameters`: invalid parameters provided to create an Address Book Wallet Address entry
- `WalletAddressValidationError`: unable to create/update an Address Book Wallet Address because the provided parameters are not conformed to the Travel Rule / Agenzia delle Entrate requirements

## Code

### iOS
```swift
let entry = CreateAddressBookEntry
    .make(
        firstName: "...",
        lastName: "...",
        label: "...",
        isWalletOwner: false,
        residenceAddress: ...,
        companyInfo: nil,
        personInfo: ...,
        isVisible: false // hidden from the address book list
    )

let walletAddress = CreateAddressBookWalletAddress
    .make(
        walletAddress: "...",
        isForeign: false,
        isUnhostedWallet: false,
        vasp: Vasp(name: "...", website: "..."),
        proofOfOwnership: nil,
        label: "...",
        threshold: nil
    )

let params = CreateAddressBookEntryWithWalletAddressParams
    .make(
        addressBook: entry,
        walletAddress: walletAddress
    )

addressBookService
    .createAddressBookEntryWithWalletAddress(params: params)
    .asPublisher()
    .sink { result in
        // ...
    }
```

### Android
```kotlin
val personInfo = AddressBookPersonInfo(
    dateOfBirth = "...",
    taxId = "..."
)

val addressBook = CreateAddressBookEntry(
    firstName = "...",
    lastName = "...",
    label = "...",
    isWalletOwner = true,
    residenceAddress = null,
    companyInfo = null,
    personInfo = personInfo,
    isVisible = false // hidden from the address book list
)

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
    threshold = FiatAmount(BigDecimal(1000))
)

val params = CreateAddressBookEntryWithWalletAddressParams(
    addressBook = addressBook,
    walletAddress = walletAddress
)

conio.addressBookService
    .createAddressBookWithWalletAddress(params)
    .asFlow()
    .collect { result ->
        //...
    }
```
