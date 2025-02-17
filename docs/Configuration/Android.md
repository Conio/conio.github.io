# Android Configuration

To use the Conio SDK, you need to create an instance of the `Conio` class, providing an Android `Context` and a  `ConioConfiguration`.

The `ConioConfiguration` allows you to specify the execution environment of the Conio SDK (e.g. test or production) and can be created with the url of the Conio Back-end and with the related Bitcoin Network.

```
val configuration = ConioConfiguration(
	// required

	baseUrl = "https://example.test.com",
	bitcoinNetwork = BitcoinNetwork.Testnet, // or BitcoinNetwork.Mainnet for production enviroment

	// optional

	// http headers added to each request, useful for debugging purposes
	headers = mapOf("header_key" to "header_value"),
)

val conio = Conio(configuration, context)
```