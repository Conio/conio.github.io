# Update Address Book Entry

## Overview

`updateAddressBookEntry` API Updates an existing address book entry. This method applies the provided changes to the address book entry identified by `addressBookId`. Only non-`nil` fields in the parameters are considered for update.

## Params

The `UpdateAddressBookEntryParams` containing the entry identifier and the fields to update. Only the provided optional fields will be updated. Fields that already contain a value cannot be modified or removed. Any parameter set to `nil` will be ignored and the corresponding value in the existing entry will remain unchanged.
 
- address book id: the unique identifier of the address book entry to update.
- label: the new label for the address book entry.
- residence address: the updated residence (geographical) address information.
- company info: the updated company information associated with the entry.
- person info: the updated personal information associated with the entry.

## Result

The `UpdateAddressBookEntryResult` containing the updated address book entry.

- updated entry: the updated address book entry.

## Code

### iOS
```swift
let params = UpdateAddressBookEntryParams.make(
    addressBookId: ...,
    label: ...,
    residenceAddress: ...,
    companyInfo: ...,
    personInfo: ...
)

addressBookService
    .updateAddressBookEntry(params: params)
    .asPublisher()
    .sink { result in
        // ...
    }
```