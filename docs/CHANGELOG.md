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

## [2.2.0](https://bitbucket.org/squadrone/conio-sdk-b2b-ios/src/2.2.0/) - 06-03-2025

### Fixed

### Added

- `BuyActivity` model properties: `cryptoCurrency`, `cryptoAmount`, `fiatAmount` and `serviceFee`
- `SellActivity` model properties: `cryptoCurrency`, `cryptoAmount`, `fiatAmount` and `serviceFee`
- `TransferActivity.miningFee` model property
- `CryptocurrencyMetadata.ConioInfo` model properties: `active` and `maintenance`
- `AskResult.cryptoCurrency` model property

### Removed

- `Transaction` model properties: `fiatAmount`, `fiatCurrency` and `serviceFee`
- `TradingSummaryResult.Stats.tradedCryptoAmount` model property
- unnecessary `PermissionType` enum cases

### Changed

- Made `BuyActivity.transaction` model property optional
- Made `SellActivity.transaction` model property optional
- Made `Transaction` model properties required (non-null)
- Renamed `Transaction.cryptoAmount` property in `netCryptoAmount`
- Renamed `MempoolStatus` model into `TransactionInclusionInfo`
- Renamed `BtcSpeedUpFeesResult.transactionMempoolStatus` property into `currentTransactionStatus`
- Renamed `BtcSpeedUpFeesResult.SpeedUpFee.mempoolStatus` property into `inclusionInfo`
- Replaced `BtcSpeedUpFeesResult.SpeedUpFee.cryptoAmount` property with `grossCryptoAmount` and `netCryptoAmount`
- Replaced `BtcTransactionFeesResult.TransactionFee.cryptoAmount` property with `grossCryptoAmount` and `netCryptoAmount`
- Replaced `CryptocurrencyMetadata.ConioInfo.cryptoType` with `chainType`
- `TransferResult.grossAmount` and `TransferResult.serviceFee` model property type from `FiatAmount` to `CryptoAmount`

## [2.1.7](https://bitbucket.org/squadrone/conio-sdk-b2b-ios/src/2.1.7/) - 27-02-2025
### Fixed
- Missing `mfa` property to `SendParams`

## [2.1.6](https://bitbucket.org/squadrone/conio-sdk-b2b-ios/src/2.1.6/) - 26-02-2025
### Fixed
- Email Mfa Challenge error parsing

## [2.1.5](https://bitbucket.org/squadrone/conio-sdk-b2b-ios/src/2.1.5/) - 10-01-2025
### Fixed
- No stored session after login with user that need to accept the new T&C

## [2.1.4](https://bitbucket.org/squadrone/conio-sdk-b2b-ios/src/2.1.4/) - 09-12-2024
### Fixed
- Swift Lint build issue

## [2.1.3](https://bitbucket.org/squadrone/conio-sdk-b2b-ios/src/2.1.3/) - 29-11-2024
### Changed
- Replaced `SignupParams.LegalAcceptance` and `LegalAcceptancesParams.LegalAcceptance` models with unified `LegalAcceptance` model
- Replaced `SignupParams.LegalAcceptanceType` and `LegalAcceptancesParams.LegalAcceptanceType` models with unified `LegalAcceptanceType` model

### Fixed
- Added missing `LegalAcceptancesResult.Acceptance.type`

## [2.1.2](https://bitbucket.org/squadrone/conio-sdk-b2b-ios/src/2.1.2/) - 22-10-2024
### Changed
- Update ConioSDK

## [2.1.1](https://bitbucket.org/squadrone/conio-sdk-b2b-ios/src/2.1.1/) - 04-10-2024
### Changed
- Update Fetch Historical Prices

## [2.1.0](https://bitbucket.org/squadrone/conio-sdk-b2b-ios/src/2.1.0/) - 18-09-2024
### Changed
- Transfer Service

## [2.0.1](https://bitbucket.org/squadrone/conio-sdk-b2b-ios/src/2.0.1/) - 07-08-2024
### Changed
- Update ConioSDK

## [2.0.0](https://bitbucket.org/squadrone/conio-sdk-b2b-ios/src/2.0.0/) - 13-06-2024
### Added
- Trading Info Service
- Btc Transaction Management Service
- Trading Buy Service
- Trading Sell Service
- Trading Price Service
- Swap Service

### Changed
- User Service
- Wallet Service

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

## [0.6.2](https://bitbucket.org/squadrone/conio-swift-sdk/src/0.6.2/) - 17-11-2021
### Changed
- Wallet service `walletPDFActivities`, `limit` in `PDFActivitiesParams` now optional
### Added
- User service `getLegalAcceptances` , new `preContractualInfoUrl` param in `LegalAcceptances` response

## [0.6.0](https://bitbucket.org/squadrone/conio-swift-sdk/src/0.6.0/) - 02-11-2021
### Added
- User service `changeEmail`

## [0.5.0](https://bitbucket.org/squadrone/conio-swift-sdk/src/0.5.0/) - 11-10-2021
### Changed
- Data serialization and mapping
- Code refactor and optimizations

## [0.4.0](https://bitbucket.org/squadrone/conio-swift-sdk/src/0.4.0/) - 13-09-2021
### Fixed
- Wrong mapping for `rangeFrom` property in `ServiceFee`
### Changed
- Update `rangeFrom` type from `UInt64?` to `FiatAmount?` in `ServiceFee`

## [0.3.3](https://bitbucket.org/squadrone/conio-swift-sdk/src/0.3.3/) - 07-09-2021
### Changed
- Rename `tradedFiat` to `weightedBidBalance` in `TradingInfo.swift` as per docs specifications

## [0.3.2](https://bitbucket.org/squadrone/conio-swift-sdk/src/0.3.2/) - 20-07-2021
### Added
- Bitcoin network `privateMainnet` and `privateTestnet`

## [0.3.1](https://bitbucket.org/squadrone/conio-swift-sdk/src/0.3.1/) - 19-07-2021
### Fixed
- Avoid using app bundle identifier during keychain init

## [0.3.0](https://bitbucket.org/squadrone/conio-swift-sdk/src/0.3.0/) - 14-07-2021
### Changed
- Added missing filters params in `ActivitiesParams` to correctly get wallet activities
- Refactor on SDK errors: `ConioError` is now the only error type throwable (check [operation](./operation/Operation.md) section)

## [0.2.0](https://bitbucket.org/squadrone/conio-swift-sdk/src/0.2.0/) - 06-07-2021
### Changed
- SDK configuration object `ConioConfiguration` has no default value and must be explicitly initialized

### Fixed
- Fix wrong privacy policies url mapping in `GetLegalAcceptancesOperation`
- Avoid build error on Xcode 12.4 in `OpenAPIConioBuilder`

## [0.1.6](https://bitbucket.org/squadrone/conio-swift-sdk/src/0.1.6/) - 25-06-2021
### Changed
- Explicit fees represented as intervals
- `WiretransferPayeeInfo` in `CreatedBid` has now two dedicated properties representing standard and custom wire transfer payee info
- `CreatedBid` now contains net cost amount `fiatAmount` and gross amount `grossFiatAmount`
- All fiat amounts are now represented as `Decimal`


## [0.1.5](https://bitbucket.org/squadrone/conio-swift-sdk/src/0.1.5/) - 15-06-2021
### Changed
- `Models` update
- `Bid`, `Ask` e `Transaction` properties linked to amount/balance now are declared with type `UInt64`

### Added
- `ConioError` entity to map operation errors

## [0.1.4](https://bitbucket.org/squadrone/conio-swift-sdk/src/0.1.4/) - 10-06-2021
### Changed
- `Models` update
 - `Bid`, `Ask`, `WalletBalances` e `SimpleActivity` properties now have public control access
 - `Bid`, `Ask`, `WalletBalances` e `SimpleActivity` properties linked to amount/balance now are declared with type `UInt64`

### Removed
- Removed `SwiftyRSA` from dependencies included in `ConioSDK`

## 0.1.3 - 03-06-2021
### Fixed
- Correzione errore signup operation

## 0.1.0 - 12-04-2021
### Added
- Rilascio versione 0.1.0

# Android

## [2.1.2](https://artifactory.conio.com/artifactory/webapp/#/artifacts/browse/tree/General/gradle-release-local/com/conio/sdk-b2b/2.1.2) - 27-02-2025

### Fixed

- Email Mfa Challenge error parsing

## [2.1.1](https://artifactory.conio.com/artifactory/webapp/#/artifacts/browse/tree/General/gradle-release-local/com/conio/sdk-b2b/2.1.1) - 05-12-2024

### Fixed

- deadlock on `UserService.signup` and `UserService.login`

### Added

- Mining fees in transfer activity

## [2.1.0](https://artifactory.conio.com/artifactory/webapp/#/artifacts/browse/tree/General/gradle-release-local/com/conio/sdk-b2b/2.1.0) - 17-10-2024

### Added

- Swap Services
- Transfer Services

### Changed

- `FetchHistoricalPricesParams` fields used to specify the timeframe to a pre-defined timestamp set

## [1.0.0](https://artifactory.conio.com/artifactory/webapp/#/artifacts/browse/tree/General/gradle-release-local/com/conio/sdk-b2b/1.0.0) - 16-07-2024

### Changed

First multicrypto SDK release

## [0.8.11](https://artifactory.conio.com/artifactory/webapp/#/artifacts/browse/tree/General/gradle-release-local/com/conio/sdk2/0.8.11) - 7-06-2022
### Added
- `ConioException.OnNetwork` to wrap network communication errors

### Fixed
- Always throw `ConioException.Unauthorized` on session expired

## [0.8.3](https://artifactory.conio.com/artifactory/webapp/#/artifacts/browse/tree/General/gradle-release-local/com/conio/sdk2/0.8.3) - 24-03-2022
### Fixed
- Initialization error caused by unusable KeyStore keys

## [0.8.0](https://artifactory.conio.com/artifactory/webapp/#/artifacts/browse/tree/General/gradle-release-local/com/conio/sdk2/0.8.0) - 9-03-2022
### Changed
- Minimum Android version supported to *Android 6.0* (Android Sdk Version: *23*)
- Improved performance
- `SellParams` deprecated

### Added
- Factory method `CreateOrRefreshAskParams.withAll` to request an Ask with the maximum sellable amount
- Model `CryptoChangeEmailParams` to replace `ChangeEmailParams`
- Model `CryptoSellParams` to replace `SellParams`

## [0.7.18](https://artifactory.conio.com/artifactory/webapp/#/artifacts/browse/tree/General/gradle-release-local/com/conio/sdk2/0.7.18) - 8-02-2022
### Changed
- Solved retro-compatibility with OkHttp 3.x
- Removed appsync dependency

## [0.7.16](https://artifactory.conio.com/artifactory/webapp/#/artifacts/browse/tree/General/gradle-release-local/com/conio/sdk2/0.7.16) - 4-02-2022
### Changed
- Downgraded OkHttp to 3.14.9

## [0.7.15](https://artifactory.conio.com/artifactory/webapp/#/artifacts/browse/tree/General/gradle-release-local/com/conio/sdk2/0.7.15) - 3-02-2022
### Changed
- Improved concurrencly on service layer
- Updated OkHttp to 4.9.0

## [0.7.13](https://artifactory.conio.com/artifactory/webapp/#/artifacts/browse/tree/General/gradle-release-local/com/conio/sdk2/0.7.13) - 24-01-2022
### Fixed
- Compatibility issue below Api level 26

## [0.7.9](https://artifactory.conio.com/artifactory/webapp/#/artifacts/browse/tree/General/gradle-release-local/com/conio/sdk2/0.7.9) - 26-11-2021
### Changed
- Legal text copies on the `LegalAcceptances` model

## [0.7.8](https://artifactory.conio.com/artifactory/webapp/#/artifacts/browse/tree/General/gradle-release-local/com/conio/sdk2/0.7.8) - 17-11-2021
### Changed
- Wallet service `activityListPdf`, `limit` in `ActivityListPdfParams` now nullable
### Added
- User service `getLegalAcceptances` , new `preContractualInfoUrl` param in `LegalAcceptances` response

## [0.7.4](https://artifactory.conio.com/artifactory/webapp/#/artifacts/browse/tree/General/gradle-release-local/com/conio/sdk2/0.7.4) - 02-11-2021
### Added
- User service `changeEmail`

## [0.7.2](https://artifactory.conio.com/artifactory/webapp/#/artifacts/browse/tree/General/gradle-release-local/com/conio/sdk2/0.7.2) - 20-10-2021
### Added
- API to get activities in PDF format

## [0.7.0](https://artifactory.conio.com/artifactory/webapp/#/artifacts/browse/tree/General/gradle-release-local/com/conio/sdk2/0.7.0) - 11-10-2021
### Changed
- Data serialization and mapping
- Code refactor and optimizations

## [0.6.2](https://artifactory.conio.com/artifactory/webapp/#/artifacts/browse/tree/General/gradle-release-local/com/conio/sdk2/0.6.2) - 03-08-2021
### Fixed
- Security issue

## [0.6.1](https://artifactory.conio.com/artifactory/webapp/#/artifacts/browse/tree/General/gradle-release-local/com/conio/sdk2/0.6.1) - 29-07-2021
### Changed
- Refactor on SDK errors: `ConioException` as the operations result error type

## [0.6.0](https://artifactory.conio.com/artifactory/webapp/#/artifacts/browse/tree/General/gradle-release-local/com/conio/sdk2/0.6.0) - 28-07-2021
### Changed
- Refactor on SDK errors: `ConioException` is now the only error type throwable (check [operation](./operation/Operation.md) section)

## [0.5.4](https://artifactory.conio.com/artifactory/webapp/#/artifacts/browse/tree/General/gradle-release-local/com/conio/sdk2/0.5.4) - 26-07-2021
### Fixed
- Made `cro`, `iban` and `chargedAt` fields of `Ask` class optional
- Made `paidAt` field of `Ask` class non-optional

## [0.5.3](https://artifactory.conio.com/artifactory/webapp/#/artifacts/browse/tree/General/gradle-release-local/com/conio/sdk2/0.5.3) - 20-07-2021
### Added
- Bitcoin network `privateMainnet` and `privateTestnet`

## [0.5.1](https://artifactory.conio.com/artifactory/webapp/#/artifacts/browse/tree/General/gradle-release-local/com/conio/sdk2/0.5.1) - 14-07-2021
### Fixed
- Fix factory methods of `TimeFrame` class

## [0.5.0](https://artifactory.conio.com/artifactory/webapp/#/artifacts/browse/tree/General/gradle-release-local/com/conio/sdk2/0.5.0) - 06-07-2021
### Changed
- SDK configuration object `ConioConfiguration` has no default value and must be explicitly initialized

## [0.4.8](https://artifactory.conio.com/artifactory/webapp/#/artifacts/browse/tree/General/gradle-release-local/com/conio/sdk2/0.4.8) - 25-06-2021
### Changed
- Explicit fees represented as intervals
- `WiretransferPayeeInfo` in `CreatedBid` has now two dedicated properties representing standard and custom wire transfer payee info
- `CreatedBid` now contains net cost amount `fiatAmount` and gross amount `grossFiatAmount`
- All fiat amounts are now represented as `BigDecimal`

### Removed
- Removed `type` property from `ServiceFee` entity
- Renamed `id` property of model entities:
    - `CreatedAsk.id` -> `CreatedAsk.askId`
    - `CreatedBid.id` -> `CreatedBid.bidId`
    - `SimpleActivity.id`  -> `SimpleActivity.activityId`
    - `ActivityDetails.id` -> `ActivityDetails.activityId`

### Added
- `ConioError`:
    - INVALID_CRYPTO_PROOF,
    - CRYPTO_PROOF_EXPIRED

## [0.4.7](https://artifactory.conio.com/artifactory/webapp/#/artifacts/browse/tree/General/gradle-release-local/com/conio/sdk2/0.4.7) - 01-06-2021
### Added
- Aggiunta di `weightedBidBalance` alle `TradingInfo`: controvalore investito
### modified
- Modifica alle `TradingFees`: supporto fasce di commissioni

## [0.4.2](https://artifactory.conio.com/artifactory/webapp/#/artifacts/browse/tree/General/gradle-release-local/com/conio/sdk2/0.4.2) - 13-04-2021
### Added
- Rilascio versione 0.4.2

## [0.4.1](https://artifactory.conio.com/artifactory/webapp/#/artifacts/browse/tree/General/gradle-release-local/com/conio/sdk2/0.4.1) - 12-04-2021
### Added
- Rilascio versione 0.4.1
