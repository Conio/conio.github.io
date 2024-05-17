# Initialize the SDK

## Conio object

The `Conio` object needs to be initialized with a `ConioConfiguration`.

You can use the `test` configuration that will connect to the staging environment and the Bitcoin testnet blockchain.
The `prod` environment instead will connect to the production server and the Bitcoin original blockchain.

You can also initialize the SDK with a custom environment, with the url of the backend and a Bitcoin blockchain.

### Parameters

- **configuration**: configuration to initialize the SDK: [ConioConfiguration](#conio-configuration) type
- (Android) **context**: context will save in the Shared Preferences

### Conio Configuration

- **identifier**: name of the configuration
- **bitcoinNetwork**: the Bitcoin network, either `.testnet` or `.mainnet`
- **networkEnvironment**: the environment (which backend): [NetworkEnvironment](#network-environment) type

### Network Environment

- **name**: name of the environment
- **host**: the host

### Code

#### Android
```java
import com.conio.sdk.Conio;
import com.conio.sdk.models.shared.BitcoinNetwork;
import com.conio.sdk.models.shared.ConioConfiguration;
import com.conio.sdk.providers.networking.NetworkEnvironment;

// Test configuration
Conio conio = new Conio(ConioConfiguration.test, getApplicationContext());

// Production configuration
Conio conio = new Conio(ConioConfiguration.prod, getApplicationContext());
```

#### iOS
```swift
import ConioSDK

// Test configuration
let conio = Conio(configuration: ConioConfiguration.test)

// Production configuration
let conio = Conio(configuration: ConioConfiguration.prod)
```
