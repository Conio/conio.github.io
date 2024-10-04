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
[]: # "Remove section if no new implementation was done ... "


# iOS
## [2.1.1](https://bitbucket.org/squadrone/conio-sdk-b2b-ios/src/2.1.1/) - 04-10-2024
### Changed
- TSK-6182: Update Fetch Historical Prices

## [2.1.0](https://bitbucket.org/squadrone/conio-sdk-b2b-ios/src/2.1.0/) - 18-09-2024
### Changed
- TSK-4511: Transfer Service

## [2.0.1](https://bitbucket.org/squadrone/conio-sdk-b2b-ios/src/2.0.1/) - 07-08-2024
### Changed
- Update ConioSDK

## [2.0.0](https://bitbucket.org/squadrone/conio-sdk-b2b-ios/src/2.0.0/) - 13-06-2024
### Added
- TSK-4503: Trading Info Service
- TSK-4504: Btc Transaction Management Service
- TSK-4505: Trading Buy Service
- TSK-4506: Trading Sell Service
- TSK-4509: Trading Price Service
- TSK-4510: Swap Service

### Changed
- TSK-4502: User Service
- TSK-4598: Wallet Service

## [0.7.0](https://bitbucket.org/squadrone/conio-swift-sdk/src/0.7.0/) - 07-06-2022
### Added
- Model `CryptoSellParams` to replace `SellParams`
- `ConioError.onNetwork` to wrap network communication errors

### Changed
- `SellParams` deprecated
- Factory init used to create/refresh an ask with all user available amount

### Fixed
- Always throw `ConioError.unauthorized` on session expired

## [0.6.10](https://bitbucket.org/squadrone/conio-swift-sdk/src/0.6.10/) - 09-02-2022
### Changed
- Update legal acceptances

## [0.6.9](https://bitbucket.org/squadrone/conio-swift-sdk/src/0.6.9/) - 08-02-2022
### Changed
- Error mapping as `unauthorized` on 401 status code

## [0.6.8](https://bitbucket.org/squadrone/conio-swift-sdk/src/0.6.8/) - 28-01-2022
### Added
- Transaction speedup
- Reset password flow APIs
- KYC create applicant params public init
- KYC trigger check params public init
- User data handling APIs
- User permissions map update
### Changed
- Updated model: withdrawal transaction, available fee
### Fixed
- Signup B2B wallet encrypt with hashed password
- Bad cancellables store in operations
- Missing password hash on B2B signup

### [0.6.2](https://bitbucket.org/squadrone/conio-swift-sdk/src/0.6.2/) - 17-11-2021
#### Changed
- Wallet service `walletPDFActivities`, `limit` in `PDFActivitiesParams` now optional
#### Added
- User service `getLegalAcceptances` , new `preContractualInfoUrl` param in `LegalAcceptances` response

### [0.6.0](https://bitbucket.org/squadrone/conio-swift-sdk/src/0.6.0/) - 02-11-2021
#### Added
- User service `changeEmail`

### [0.5.0](https://bitbucket.org/squadrone/conio-swift-sdk/src/0.5.0/) - 11-10-2021
#### Changed
- Data serialization and mapping
- Code refactor and optimizations

### [0.4.0](https://bitbucket.org/squadrone/conio-swift-sdk/src/0.4.0/) - 13-09-2021
#### Fixed
- Wrong mapping for `rangeFrom` property in `ServiceFee`
#### Changed
- Update `rangeFrom` type from `UInt64?` to `FiatAmount?` in `ServiceFee`

### [0.3.3](https://bitbucket.org/squadrone/conio-swift-sdk/src/0.3.3/) - 07-09-2021
#### Changed
- Rename `tradedFiat` to `weightedBidBalance` in `TradingInfo.swift` as per docs specifications

### [0.3.2](https://bitbucket.org/squadrone/conio-swift-sdk/src/0.3.2/) - 20-07-2021
#### Added
- Bitcoin network `privateMainnet` and `privateTestnet`

### [0.3.1](https://bitbucket.org/squadrone/conio-swift-sdk/src/0.3.1/) - 19-07-2021
#### Fixed
- Avoid using app bundle identifier during keychain init

### [0.3.0](https://bitbucket.org/squadrone/conio-swift-sdk/src/0.3.0/) - 14-07-2021
#### Changed
- Added missing filters params in `ActivitiesParams` to correctly get wallet activities
- Refactor on SDK errors: `ConioError` is now the only error type throwable (check [operation](./operation/Operation.md) section)

### [0.2.0](https://bitbucket.org/squadrone/conio-swift-sdk/src/0.2.0/) - 06-07-2021
#### Changed
- SDK configuration object `ConioConfiguration` has no default value and must be explicitly initialized

#### Fixed
- Fix wrong privacy policies url mapping in `GetLegalAcceptancesOperation`
- Avoid build error on Xcode 12.4 in `OpenAPIConioBuilder`

### [0.1.6](https://bitbucket.org/squadrone/conio-swift-sdk/src/0.1.6/) - 25-06-2021
#### Changed
- Explicit fees represented as intervals
- `WiretransferPayeeInfo` in `CreatedBid` has now two dedicated properties representing standard and custom wire transfer payee info
- `CreatedBid` now contains net cost amount `fiatAmount` and gross amount `grossFiatAmount`
- All fiat amounts are now represented as `Decimal`


### [0.1.5](https://bitbucket.org/squadrone/conio-swift-sdk/src/0.1.5/) - 15-06-2021
#### Changed
- `Models` update
- `Bid`, `Ask` e `Transaction` properties linked to amount/balance now are declared with type `UInt64`

#### Added
- `ConioError` entity to map operation errors

### [0.1.4](https://bitbucket.org/squadrone/conio-swift-sdk/src/0.1.4/) - 10-06-2021
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

### [0.8.11](https://bitbucket.org/squadrone/conio-android-sdk2/src/43ddfec2fec7ad8bd5444eaae48483ae33eec68d/?at=release%2F0.8.11) - 7-06-2022
#### Added
- `ConioException.OnNetwork` to wrap network communication errors

#### Fixed
- Always throw `ConioException.Unauthorized` on session expired

### [0.8.3](https://bitbucket.org/squadrone/conio-android-sdk2/src/0bc388e1f93bd5a211b8d629aeeee224c7770429/?at=release%2F0.8.3) - 24-03-2022
#### Fixed
- Initialization error caused by unusable KeyStore keys

### [0.8.0](https://bitbucket.org/squadrone/conio-android-sdk2/src/5f941a03e044c7cf518ca8ef6b0de5768bf56067/?at=release%2F0.8.0) - 9-03-2022
#### Changed
- Minimum Android version supported to *Android 6.0* (Android Sdk Version: *23*)
- Improved performance
- `SellParams` deprecated

#### Added
- Factory method `CreateOrRefreshAskParams.withAll` to request an Ask with the maximum sellable amount
- Model `CryptoChangeEmailParams` to replace `ChangeEmailParams`
- Model `CryptoSellParams` to replace `SellParams`

### [0.7.18](https://bitbucket.org/squadrone/conio-android-sdk2/src/ae6273eb37b40d1daead7cdda9f218abd95224c6/?at=release%2F0.7.18) - 8-02-2022
#### Changed
- Solved retro-compatibility with OkHttp 3.x
- Removed appsync dependency

### [0.7.16](https://bitbucket.org/squadrone/conio-android-sdk2/src/f9767748347ef76b94022cf704c2b7ac166e5cb7/?at=release%2F0.7.16) - 4-02-2022
#### Changed
- Downgraded OkHttp to 3.14.9

### [0.7.15](https://bitbucket.org/squadrone/conio-android-sdk2/src/3c83fd26a3c17c33b1f330cf4d896068341d89a8/?at=release%2F0.7.15) - 3-02-2022
#### Changed
- Improved concurrencly on service layer
- Updated OkHttp to 4.9.0

### [0.7.13](https://bitbucket.org/squadrone/conio-android-sdk2/src/94c4223c400d31d89dda595ac3acf601c26c2ea2/?at=release%2F0.7.13) - 24-01-2022
#### Fixed
- Compatibility issue below Api level 26

### [0.7.9](https://bitbucket.org/squadrone/conio-android-sdk2/src/c510c7a12e27f362b291e2f9711d376e3f8dbbbc/?at=release%2F0.7.9) - 26-11-2021
#### Changed
- Legal text copies on the `LegalAcceptances` model

### [0.7.8](https://bitbucket.org/squadrone/conio-android-sdk2/src/20827d74d45354d62230a4ea6a11f649c44e1f24/?at=release%2F0.7.8) - 17-11-2021
#### Changed
- Wallet service `activityListPdf`, `limit` in `ActivityListPdfParams` now nullable
#### Added
- User service `getLegalAcceptances` , new `preContractualInfoUrl` param in `LegalAcceptances` response

### [0.7.4](https://bitbucket.org/squadrone/conio-android-sdk2/src/f29a930a953cdeb04a189a04f05a7db210e517b6/?at=release%2F0.7.4) - 02-11-2021
#### Added
- User service `changeEmail`

### [0.7.2](https://bitbucket.org/squadrone/conio-android-sdk2/src/d2802e047e511fefcb0ce9f1807be8e38742e70d/?at=release%2F0.7.2) - 20-10-2021
#### Added
- API to get activities in PDF format

### [0.7.0](https://bitbucket.org/squadrone/conio-android-sdk2/src/3a22f23b0ff1a07972e4da5477c86fa98d34ef72/?at=release%2F0.7.0) - 11-10-2021
#### Changed
- Data serialization and mapping
- Code refactor and optimizations

### [0.6.2](https://bitbucket.org/squadrone/conio-android-sdk2/src/922c216dadc71aada864a538e34d5b62a256850f/?at=release%2F0.6.2) - 03-08-2021
#### Fixed
- Security issue

### [0.6.1](https://bitbucket.org/squadrone/conio-android-sdk2/src/300349f7414b4c6abac14f91d50573262116a553/?at=release%2F0.6.1) - 29-07-2021
#### Changed
- Refactor on SDK errors: `ConioException` as the operations result error type

### [0.6.0](https://bitbucket.org/squadrone/conio-android-sdk2/src/f95b063d89f7d3dfda8871e36c718a1031e861af/?at=release%2F0.6.0) - 28-07-2021
#### Changed
- Refactor on SDK errors: `ConioException` is now the only error type throwable (check [operation](./operation/Operation.md) section)

### [0.5.4](https://bitbucket.org/squadrone/conio-android-sdk2/src/06d77afb5153e52f696b33d5df9329e47110b01a/?at=release%2F0.5.4) - 26-07-2021
#### Fixed
- Made `cro`, `iban` and `chargedAt` fields of `Ask` class optional
- Made `paidAt` field of `Ask` class non-optional

### [0.5.3](https://bitbucket.org/squadrone/conio-android-sdk2/src/0d60053a9a1bf149cafb8a3e54200a53da2e17bf/?at=release%2F0.5.3) - 20-07-2021
#### Added
- Bitcoin network `privateMainnet` and `privateTestnet`

### [0.5.1](https://bitbucket.org/squadrone/conio-android-sdk2/src/aa74590d773e9320cfa62a23425f09c1e8234c54/?at=release%2F0.5.1) - 14-07-2021
#### Fixed
- Fix factory methods of `TimeFrame` class

### [0.5.0](https://bitbucket.org/squadrone/conio-android-sdk2/src/1203815eb2c6e97274b22d1e8521b14604577b55/?at=release%2F0.5.0) - 06-07-2021
#### Changed
- SDK configuration object `ConioConfiguration` has no default value and must be explicitly initialized

### [0.4.8](https://bitbucket.org/squadrone/conio-android-sdk2/src/071f4deb885f003fb9d65bb9d9f79a5adff1fac5/?at=release%2F0.4.8) - 25-06-2021
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

### [0.4.7](https://bitbucket.org/squadrone/conio-android-sdk2/src/5d71792b29a83e72c6342f658fe8920352a1296b/?at=release%2F0.4.7) - 01-06-2021
#### Added
- Aggiunta di `weightedBidBalance` alle `TradingInfo`: controvalore investito
#### modified
- Modifica alle `TradingFees`: supporto fasce di commissioni

### [0.4.2](https://bitbucket.org/squadrone/conio-android-sdk2/src/b0cdb3f801c410b12e8478b434e559256b3ac264/?at=release%2F0.4.2) - 13-04-2021
#### Added
- Rilascio versione 0.4.2

### [0.4.1](https://bitbucket.org/squadrone/conio-android-sdk2/src/e3d4d6d5fe4778aff99b5a72ead9316f9e0ef581/?at=release%2F0.4.1) - 12-04-2021
#### Added
- Rilascio versione 0.4.1
