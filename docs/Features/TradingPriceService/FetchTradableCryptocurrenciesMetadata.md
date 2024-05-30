# Fetch Tradable Crypto Metadata

## Overview
---
`fetchTradableCryptoMetadata` API is used to retrieve metadata about all tradable cryptocurrencies. It allows client to fetch the tradable cryptocurrencies metadata with information such as cryptocurrency short name, image, symbol, slug, supply, market data and more.

## Params
---
The `FetchTradableCryptoMetadataParams` used to initialize and perform `fetchTradableCryptoMetadata` API.

- language code: The ISO language code and ISO country code (language_COUNTRY) used to retrieve tradable cryptocurrencies descriptions

## Result
---
The `TradableCryptoMetadataResult` data with all tradable cryptocurrencies metadata.

- metadata: the tradable cryptocurrencies `CryptoCurrencyMetadata` list

## Code
---
### iOS
```swift
let params = FetchTradableCryptoMetadataParams.makeItalian()

tradingPriceService
	.fetchTradableCryptoMetadata()
	.asPublisher()
	.sink { result in 
		// ...
	}

```

### Android
```kotlin
// val language = Language.Italian
val language = Language.English

val params = FetchCryptoCurrenciesMetadataParams(
    language = language
)

conio.tradingPriceService
    .fetchCryptoCurrenciesMetadata(params)
    .asFlow()
    .collect { result ->
        // ...
    }
```