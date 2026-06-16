# Search Address Book Entries

## Overview

`searchAddressBookEntries` API searches address book entries across names, labels, wallet addresses, and company names.

## Params

The `SearchAddressBookEntriesParams` used to initialize and perform `searchAddressBookEntries` API.

- search text: search text to filter address book entries by name. If empty string (`""`), returns the complete address book list.

## Result

The `SearchAddressBookEntriesResult` contains the `FullAddressBookEntry` list.

- entries: array of complete address book entries matching the search criteria. Each entry includes full contact details + associated wallet addresses.

## Code

### iOS
```swift
let params = SearchAddressBookEntriesParams.make(searchText: ...)

addressBookService
    .searchAddressBookEntries(params: params)
    .asPublisher()
    .sink { result in
        // ...
    }
```

### Android
```kotlin
val params = SearchAddressBookEntriesParams(
    searchText= "..."
)

conio.addressBookService
    .searchAddressBookEntries(params)
    .asFlow()
    .collect { result -> 
        //...
    }
```