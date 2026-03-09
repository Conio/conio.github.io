# Get Vasp List

## Overview

`getVaspList` API fetches the list of available VASPs.

## Result

The `VaspListResult` containing the retrieved VASP list.

- vasp list: the list of Virtual Asset Service Providers (VASPs).

## Code

### iOS
```swift 
addressBookService
    .getVaspList()
    .asPublisher()
    .sink { result in
        // ...
    }
```