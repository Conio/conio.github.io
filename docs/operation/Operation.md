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

### ConioError (iOS)

Questo errore raggruppa tutte le possibili risposte di errore direttamente legate alle operazioni.

```swift

// General operation error with name and/or description
case onOperation(String)
// Decoding data error
case unableToDecodeData
// Cryptographic operation error
case onCryptography
// Secure storage operation error
case onStorage
// OAuth flow error: unable to retrieve and/or refresh access token
case unauthorized
// TBD
case appImprovementAcceptanceNotAccepted
// TBD
case clientSupportAcceptanceNotAccepted
// Ask operation already paid
case askAlreadyPaid
// Bid operation already paid
case bidAlreadyPaid
// Bid operation is expired
case bidExpired
// TBD
case bidIsInError
// Bid operation is not yet paid
case bidNotYetPaid
case bithustlerServiceCouldNotCreateSeller
// TBD
case cardsLimitsExceeded
case cardsServiceCouldNotCreatePayer
case duplicateEmailAddress
case dustAsk
case dustTransaction
// Fiat amount is under the minumum level limit
case fiatAmountTooLow
case inconsistentState
case inconsistentTransaction
case invalidIban
case invalidMessageSignature
// Used payment method is not valid
case invalidPaymentMethod
case invalidToken
case invalidTokenPayload
// Crypto proof used for operation is invalid
case invalidCryptoProof
case multipleSellMethods
case noSuch3DSecure
case noSuchSellMethod
// TBD
case noSuchSeller
// TBD
case noSuchWallet
case noSuchWithdrawalFeesInfo
case notEnoughBtcAmount
case tradeExpired
// Bid operation exceeded user purchase max limits
case tradingLimitsExceeded
case unavailableBtcSubsystem
// Ask operation is in an error status
case unrecoverableAsk
// Bid operation is in an error status
case unrecoverableBid
// Payment method used in not supported
case unsupportedPaymentMethod
case walletAlreadyCreatedWithDifferentKeys
case walletAlreadyOwnedByAnotherUser
// Unknown error with description
case unknown(String)
// Conio SDK version is outdated
case outdatedSdk
// Server is under maintenance
case underMaintenance
```

### ConioException (Android)

Questo errore raggruppa (sia come namespace che come supertipo) tutte le possibili risposte di errore direttamente legate alle operazioni.

```kotlin
sealed class ConioException : Exception {
    // General operation error with name and/or description
    class OnOperation : ConioException
    // Decoding data error
    class UnableToDecodeData : ConioException
    // Cryptographic operation error
    class OnCryptography : ConioException
    // Secure storage operation error
    class OnStorage : ConioException
    // OAuth flow error: unable to retrieve and/or refresh access token
    class Unauthorized : ConioException
    // Conio SDK version is outdated
    class OutdatedSdk : ConioException
    // Server is under maintenance
    class UnderMaintenance : ConioException


    class AppImprovementAcceptanceNotAccepted : ConioException

    class ClientSupportAcceptanceNotAccepted : ConioException
    // Ask operation already paid
    class AskAlreadyPaid : ConioException
    // Bid operation already paid
    class BidAlreadyPaid : ConioException
    // Bid operation is expired
    class BidExpired : ConioException

    class BidIsInError : ConioException
    // Bid operation is not yet paid
    class BidNotYetPaid : ConioException

    class BithustlerServiceCouldNotCreateSeller : ConioException

    class CardsLimitsExceeded : ConioException

    class CardsServiceCouldNotCreatePayer : ConioException

    class DuplicateEmailAddress : ConioException

    class DustAsk : ConioException

    class DustTransaction : ConioException
    // Fiat amount is under the minumum level limit
    class FiatAmountTooLow : ConioException

    class InconsistentState : ConioException

    class InconsistentTransaction : ConioException

    class InvalidIban : ConioException

    class InvalidMessageSignature : ConioException
    // Used payment method is not valid
    class InvalidPaymentMethod : ConioException

    class InvalidToken : ConioException

    class InvalidTokenPayload : ConioException
    // Crypto proof used for operation is invalid
    class InvalidCryptoProof : ConioException

    class MultipleSellMethods : ConioException

    class NoSuch3DSecure : ConioException

    class NoSuchSellMethod : ConioException

    class NoSuchSeller : ConioException

    class NoSuchWallet : ConioException

    class NoSuchWithdrawalFeesInfo : ConioException

    class NotEnoughBtcAmount : ConioException

    class TradeExpired : ConioException
    // Bid operation exceeded user purchase max limits
    class TradingLimitsExceeded : ConioException

    class UnavailableBtcSubsystem : ConioException
    // Ask operation is in an error status
    class UnrecoverableAsk : ConioException
    // Bid operation is in an error status
    class UnrecoverableBid : ConioException
    // Payment method used in not supported
    class UnsupportedPaymentMethod : ConioException

    class WalletAlreadyCreatedWithDifferentKeys : ConioException

    class WalletAlreadyOwnedByAnotherUser : ConioException
    // Unknown error with description
    class Unknown : ConioException
}
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
        if (error instanceof ConioException.Unauthorized) {
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
        if (error instanceof ConioException.OutdatedSdk) {
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
        if case .outdatedSdk = error {
            print("Please update the SDK")
        }
    }
}
```
