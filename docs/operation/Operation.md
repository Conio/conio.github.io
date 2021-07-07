# Operazioni

## Introduzione

Una volta [inizializzato l'oggetto Conio](../configuration/Configuration.md), i servizi offerti dal SDK sono raggruppati in 3 categorie:

1. [Servizi dell'utente](../user/User.md) (`conio.userService.*`);
2. [Servizi del wallet](../wallet/Wallet.md) (`conio.walletService.*`);
3. [Servizi di mercato](../exchange/Exchange.md) (`conio.exchangeService.*`).

Ogni servizio è un metodo il cui valore di ritorno è un implementazione dell'interfaccia [`ServiceConsumer<O>`](#ServiceConsumer).

## ServiceConsumer

L'interfaccia `ServiceConsumer<O>` (generica in `O`, il tipo che rappresenta il risultato del servizio stesso) dichiara le modalità con cui i risultati dei servizi possono essere fruiti, infatti espone i metodi:

- `asCallbeck`, che richiede come parametro una callback che verrà invocata con il risultato del servizio;
- (Android) `asFlow`, che restituisce un oggetto di tipo [Flow](https://developer.android.com/kotlin/flow), più adatto al paradigma di programmazione reattiva;
- (iOS) `asPublisher`, TODO.

#### Code

##### Android (Java)

```java
conio.walletService.currentBitcoinAddress().asCallback(result -> result.analysis(
        address -> { /* ... */ },
        error -> { /* ... */ }
));
```

##### Android (Kotlin)

```kotlin
runBlocking {
    conio.walletService.currentBitcoinAddress().asFlow().first().analysis(
            { address -> /* ... */ },
            { error -> /* ... */ }
    )
}
```

<!-- TODO: iOS
##### iOS
-->

## Eccezioni possibili

### ConioError

Questo errore raggruppa tutte le possibili risposte di errore direttamente legate alle operazioni.

Lista dei possibili ConioError:

```
APP_IMPROVEMENT_ACCEPTANCE_NOT_ACCEPTED
ASK_ALREADY_PAID
BID_ALREADY_PAID
BID_EXPIRED
BID_IS_IN_ERROR
BID_NOT_YET_PAID
BITHUSTLER_SERVICE_COULD_NOT_CREATE_SELLER
CARDS_LIMITS_EXCEEDED
CARDS_SERVICE_COULD_NOT_CREATE_PAYER
CLIENT_SUPPORT_ACCEPTANCE_NOT_ACCEPTED
CRYPTO_PROOF_EXPIRED
DUPLICATE_EMAIL_ADDRESS
DUST_ASK
DUST_TRANSACTION
FIAT_AMOUNT_TOO_LOW
INCONSISTENT_STATE
INCONSISTENT_TRANSACTION
INVALID_CRYPTO_PROOF
INVALID_IBAN
INVALID_MESSAGE_SIGNATURE
INVALID_PAYMENT_METHOD
INVALID_TOKEN
INVALID_TOKEN_PAYLOAD
MULTIPLE_SELL_METHODS
NO_SUCH3D_SECURE
NO_SUCH_SELL_METHOD
NO_SUCH_SELLER
NO_SUCH_WALLET
NO_SUCH_WITHDRAWAL_FEES_INFO
NOT_ENOUGH_BTC_AMOUNT
TRADE_EXPIRED
TRADING_LIMITS_EXCEEDED
UNAVAILABLE_BTC_SUBSYSTEM
UNRECOVERABLE_ASK
UNRECOVERABLE_BID
UNSUPPORTED_PAYMENT_METHOD
WALLET_ALREADY_CREATED_WITH_DIFFERENT_KEYS
WALLET_ALREADY_OWNED_BY_ANOTHER_USER
```

Ad esempio, prendiamo l'operazione `conio.walletService.withdrawalFees`: se un utente ha 1 bitcoin nel portafoglio e richiede le mining fees per un invio da 50 bitcoin, riceverà un `NO_SUCH_WITHDRAWAL_FEES_INFO`.

#### Code

##### Android

```java
WithdrawalFeesParams params = new WithdrawalFeesParams(
    "mkHS9ne12qx9pS9VojpwU5xtRd4T7X7ZUt",
    100000000,
    TransactionSpeedType.SPEED_FIVE
);

conio.walletService.withdrawalFees(params).asCallback(result -> result.analysis(
        fees -> { /* ... */ },
        error -> {
            ConioException conioException = (ConioException) error;
            if (conioException.getConioError() == ConioError.NO_SUCH_WITHDRAWAL_FEES_INFO) {
                /* Handle NO_SUCH_WITHDRAWAL_FEES_INFO error */
            }
        }
));
```

### Non autorizzato

Questo errore viene generato quando non si è autorizzati a utilizzare un metodo per uno dei seguenti motivi:

- utilizzo di un metodo che richiede autenticazione senza una sessione valida;
- si sta provando ad effettura una login con credenziali errate.

Assicurarsi di avere una sessione valida, autenticandosi nuovamente tramite una [login](../user/User.md#login) o una [sign-up](../user/User.md#signup).

#### Codice

##### Android

```java
UserLogin user = new UserLogin("username", "wrong_password");

conio.userService.login(user).asCallback(result -> result.analysis(
    success -> { /* ... */ },
    error -> {
        if (error instanceof UnauthorizedException) {
            /* Handle the error */
        }

        // Or

        ServiceException serviceException = (ServiceException) error;
        if (serviceException.getServiceError() == ServiceError.UNAUTHORIZED) {
            /* Handle the error */
        }
    }
));

```

### SDK obsoleto

Questo errore viene generato quando l'utente tenta di utilizzare una versione obsoleta dell'SDK.

Consigliamo di gestire questo errore per notificare all'utente di aggiornare l'applicazione.

#### Code

##### Android

```java
LegalAcceptancesParams params = new LegalAcceptancesParams(Language.ITALIAN);

conio.userService.getLegalAcceptances(params).asCallback(result -> result.analysis(
    acceptances -> { /* ... */ },
    error -> {
        if (error instanceof OutdatedSDKException) {
            /* Handle the error */
        }

        // Or

        ServiceException serviceException = (ServiceException) error;
        if (serviceException.getServiceError() == ServiceError.OUTDATED_SDK) {
            /* Handle the error */
        }
    }
));
```

##### iOS

```swift
let params = LegalAcceptancesParams(language: .italian)

conio.userService.getLegalAcceptances(params: params).asCallback { result in
    switch result {
    case .success:
        // success
    case .failure(let error):
        if case .outdatedSDK = error {
            print("Please update the SDK")
        }
    }
}
```
