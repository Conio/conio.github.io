# Inizializzazione dell'SDK

## L'oggetto Conio

Per usare l'SDK, occorre inizializzare l'oggetto `Conio` con una `ConioConfiguration`. La configurazione determinerà l'ambiente con il quale l'SDK interagirà.

È necessario inizializzare l'SDK con un ambiente personalizzato, specificando l'url del backend e la rete Bitcoin da utilizzare.

Di seguito le specifiche per inizializzare un oggetto di tipo `Conio`.

### Parametri: **Conio**

- **configuration**: di tipo [ConioConfiguration](#parametri-conioconfiguration), la configurazione per inizializzare l'SDK;
- (Android) **context**: di tipo `Context`, il context dell'applicazione Android.

### Parametri: ConioConfiguration

- **baseUrl**: di tipo `String`, url del backend;
- **bitcoinNetwork**: di tipo `BitcoinNetwork`, la rete Bitcoin. Può essere `.testnet`, `.mainnet`, `privateMainnet` o `privateTestnet`.

### Codice

#### Android
```java
import com.conio.sdk.Conio;
import com.conio.sdk.models.shared.BitcoinNetwork;
import com.conio.sdk.models.shared.ConioConfiguration;
import com.conio.sdk.providers.networking.NetworkEnvironment;

// Test configuration
ConioConfiguration testConfig = new ConioConfiguration("https://example.test.com", BitcoinNetwork.TESTNET);
Conio conio = new Conio(testConfig, context);

// Production configuration
ConioConfiguration config = new ConioConfiguration("https://example.production.com", BitcoinNetwork.MAINNET);
Conio conio = new Conio(config, context);
```

#### iOS
```swift
import ConioSDK

// Test configuration
let testConfig = ConioConfiguration(
    withBaseUrl: "https://example.test.com",
    bitcoinNetwork: .testnet
)
let conio = Conio(config: testConfig)

// Production configuration
let config = ConioConfiguration(
    withBaseUrl: "https://example.production.com",
    bitcoinNetwork: .testnet
)
let conio = Conio(config: config)
```
