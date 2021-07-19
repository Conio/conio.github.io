# Changelog

[]: # "The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/\), and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html\)."


* [iOS](#ios)
* [Android](#android)

[]: # "NOT THE BEST WAY TO COMMENT BUT BITBUCKET MARKDOWN INTERPRETER SEEMS TO BE PRETTY MUCH STUPID"
[]: # "Format template"
[]: # "### x.y.z - dd-MM-AAAA"
[]: # "#### Added"
[]: # "... List all stuff possibly added."
[]: # "Remove section if no new implementation was done ..."
[]: # "#### Changed"
[]: # "... List all stuff possibly modified and/or updated."
[]: # "Remove section if no new implementation was done ..."
[]: # "#### Fixed"
[]: # "... List all stuff possibly fixed."
[]: # "Remove section if no new implementation was done ..."
[]: # "#### Removed"
[]: # "... List all stuff possibly removed and/or deleted."
[]: # "Remove section if no new implementation was done ... )"


## iOS

### [0.3.1] - 19-07-2021
#### Fixed
- Avoid using app bundle identifier during keychain init

### [0.3.0] - 14-07-2021
#### Changed
- Added missing filters params in `ActivitiesParams` to correctly get wallet activities
- Refactor on SDK errors: `ConioError` is now the only error type throwable (check [operation](/operation/Operation.md) section)

### [0.2.0] - 06-07-2021
#### Changed
- SDK configuration object `ConioConfiguration` has no default value and must be explicitly initialized

#### Fixed
- Fix wrong privacy policies url mapping in `GetLegalAcceptancesOperation`
- Avoid build error on Xcode 12.4 in `OpenAPIConioBuilder`

### [0.1.6] - 25-06-2021
#### Changed
- Explicit fees represented as intervals
- `WiretransferPayeeInfo` in `CreatedBid` has now two dedicated properties representing standard and custom wire transfer payee info
- `CreatedBid` now contains net cost amount `fiatAmount` and gross amount `grossFiatAmount`
- All fiat amounts are now represented as `Decimal`


### [0.1.5] - 15-06-2021
#### Changed
- `Models` update
- `Bid`, `Ask` e `Transaction` properties linked to amount/balance now are declared with type `UInt64`

#### Added
- `ConioError` entity to map operation errors

### [0.1.4] - 10-06-2021
#### Changed
- `Models` update
 - `Bid`, `Ask`, `WalletBalances` e `SimpleActivity` properties now have public control access
 - `Bid`, `Ask`, `WalletBalances` e `SimpleActivity` properties linked to amount/balance now are declared with type `UInt64`

#### Removed
- Removed `SwiftyRSA` from dependencies included in `ConioSDK`

### 0.1.3 - 03-06-2021
#### Fixed
- Correzione errore signup operation

### 0.1.0 - 12-04-2021
#### Added
- Rilascio versione 0.1.0

## Android

### [0.5.1] - 14-07-2021
#### Fixed
- Fix factory methods of `TimeFrame` class

### [0.5.0] - 06-07-2021
#### Changed
- SDK configuration object `ConioConfiguration` has no default value and must be explicitly initialized

### [0.4.8] - 25-06-2021
#### Changed
- Explicit fees represented as intervals
- `WiretransferPayeeInfo` in `CreatedBid` has now two dedicated properties representing standard and custom wire transfer payee info
- `CreatedBid` now contains net cost amount `fiatAmount` and gross amount `grossFiatAmount`
- All fiat amounts are now represented as `BigDecimal`

#### Removed
- Removed `type` property from `ServiceFee` entity
- Renamed `id` property of model entities:
    - `CreatedAsk.id` -> `CreatedAsk.askId`
    - `CreatedBid.id` -> `CreatedBid.bidId`
    - `SimpleActivity.id`  -> `SimpleActivity.activityId`
    - `ActivityDetails.id` -> `ActivityDetails.activityId`

#### Added
- `ConioError`:
    - INVALID_CRYPTO_PROOF,
    - CRYPTO_PROOF_EXPIRED

### [0.4.7] - 01-06-2021
#### Added
- Aggiunta di `weightedBidBalance` alle `TradingInfo`: controvalore investito
#### modified
- Modifica alle `TradingFees`: supporto fasce di commissioni

### [0.4.2] - 13-04-2021
#### Added
- Rilascio versione 0.4.2

### [0.4.1] - 12-04-2021
#### Added
- Rilascio versione 0.4.1


[]: # "iOS tags"
[0.3.1]: https://bitbucket.org/squadrone/conio-swift-sdk/src/0.3.1/
[0.3.0]: https://bitbucket.org/squadrone/conio-swift-sdk/src/0.3.0/
[0.2.0]: https://bitbucket.org/squadrone/conio-swift-sdk/src/0.2.0/
[0.1.6]: https://bitbucket.org/squadrone/conio-swift-sdk/src/0.1.6/
[0.1.5]: https://bitbucket.org/squadrone/conio-swift-sdk/src/0.1.5/
[0.1.4]: https://bitbucket.org/squadrone/conio-swift-sdk/src/0.1.4/

[]: # "Android tags"
[0.5.1]: https://bitbucket.org/squadrone/conio-android-sdk2/src/aa74590d773e9320cfa62a23425f09c1e8234c54/?at=release%2F0.5.1
[0.5.0]: https://bitbucket.org/squadrone/conio-android-sdk2/src/1203815eb2c6e97274b22d1e8521b14604577b55/?at=release%2F0.5.0
[0.4.8]: https://bitbucket.org/squadrone/conio-android-sdk2/src/071f4deb885f003fb9d65bb9d9f79a5adff1fac5/?at=release%2F0.4.8
[0.4.7]: https://bitbucket.org/squadrone/conio-android-sdk2/src/5d71792b29a83e72c6342f658fe8920352a1296b/?at=release%2F0.4.7
[0.4.2]: https://bitbucket.org/squadrone/conio-android-sdk2/src/b0cdb3f801c410b12e8478b434e559256b3ac264/?at=release%2F0.4.2
[0.4.1]: https://bitbucket.org/squadrone/conio-android-sdk2/src/e3d4d6d5fe4778aff99b5a72ead9316f9e0ef581/?at=release%2F0.4.1
