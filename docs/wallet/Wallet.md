# Operazioni sul portafoglio

## Indirizzo Bitcoin attuale

Permette di recuperare l'indirizzo corrente del portafoglio su cui sarà possibile ricevere delle transazioni.

### Metodo

`walletService.currentBitcoinAddress`

### Risposta

Una `stringa` contenente l'indirizzo Bitcoin attuale.

### Errori

- [Non autorizzato](../operation/Operation.md#Non-autorizzato)

### Codice

#### Android

```java
conio.walletService.currentBitcoinAddress()
    .asCallback(result -> result.analysis(
        address -> {/* Handle string wallet address */ },
        error -> { /* ... */ }
    ));
```

#### iOS

```swift
conio.walletService.currentBitcoinAddress().asCallback { result in
    switch result {
    case .success(let address):
        // Handle string wallet address
    case .failure(let error):
        // Operation Error
    }
}
```


## Lista movimenti bitcoin

Ciascuna operazione di invio, ricezione, acquisto e vendita di Bitcoin è rappresentata da un'`Activity`. La lista delle attività svolte dall'utente può essere recuperata tramite l'apposito metodo.

### Metodo

`walletService.activityList`

### Parametri

Un oggetto di tipo `ActivityListParams` contenente:

- **types**: di tipo `List<ActivityType>`, una lista di enumerati `ActivityType` che ci permette di specificare le tipologie di activities da recuperare. Tramite `ActivityType.all()` è possibile ottenere una lista di tutte le tipologie di *Activity*;

- **currency**: di tipo `Currency`, la valuta nella quale si vuole conoscere il valore della transazioni di acquisto e vendita (attualmente solo Euro);

- **@Default(6) limit**: di tipo `intero`, il numero massimo di transazioni da ricevere nella risposta;

- **@Opzionale nextPage**: di tipo `String`, token per la paginazione delle activities, ottenibile tramite il risultato di una prima richiesta di *lista movimenti* con questo valore nullo. Inserendo tale valore è possibile ottenere le successive `n` *Activity* (con `n` = valore inserito come **limit**);

- **@Opzionale timeFrame**: di tipo `TimeFrame`, la finestra temporale che definisce quali *Activity* includere nella risposta.

### Risposta

Un oggetto di tipo `ActivityList` contenente:

- **activities**: di tipo `List<SimpleActivity>`, ovvero la lista delle *Activity* dell'utente richieste;

- **@Opzionale nextPage**: di tipo `String`, token per la paginazione delle activity, che può essere inserito in una successiva richiesta di *lista movimenti*. Quando questo campo è nullo, significa che non esistono ulteriori *Activity* tra quelle che rispettano i filtri inseriti.

Ogni *Activity* resituita (di tipo `SimpleActivity`) contiene:

- **activityId**: di tipo `String`, l'identificativo univoco della *Activity*;

- **type**: di tipo `ActivityType`, la tipologia di *Activity* (`SEND`, `BUY`, `SELL`, `RECEIVE`);

- **status**: di tipo `TransactionStatus`, lo stato di conferma della transazione Bitcoin legata all'*Activity* (`UNCONFIRMED`, `PARTIALLY_CONFIRMED`, `CONFIRMED`);

- **createdAt**: di tipo `long`, l'istante temporale in cui è stata creata l'*Activity*, espresso come Unix Timestamp in millisecondi.

- **cryptoAmount**: di tipo `long`, l'ammontare in **satoshi** (1 bitcoin = 100.000.000 satoshi), movimentato dall'*Activity*;

- **fiatAmount**: di tipo `Decimal` (iOS) / `BigDecimal` (Android), il corrispettivo ammontare di **cryptoAmount**, calcolato nella valuta indicata tramite il campo **currency**;

### Errori

- [Non autorizzato](../operation/Operation.md#Non-autorizzato)

### Codice

#### Android

```java
// Example 1: retrieve 6 activities of all type
List<ActivityType> types = ActivityType.all;
ActivityListParams params = new ActivityListParams(types, Currency.EUR);

// Example 2: retrieve 10 sell activities
List<ActivityType> types = Collections.singletonList(ActivityType.SELL);
ActivityListParams params = new ActivityListParams(types, Currency.EUR, 10);

// Example 3: retrieve 6 buy and receive activities of the last month
List<ActivityType> types = Arrays.asList(ActivityType.BUY, ActivityType.RECEIVE);
ActivityListParams params = new ActivityListParams(
    types,                // types
    Currency.EUR,         // currency
    6,                    // limit
    null,                 // nextPage
    TimeFrame.lastMonth() // timeFrame
);

conio.walletService.activityList(params)
    .asCallback(result -> result.analysis(
        activityList -> { /* Handle ActivityList */ },
        error -> { /* ... */ }
    ));
```

#### iOS

```swift
let types = WalletActivityType.allCases
let params = ActivitiesParams(nextPage: "string", types: types)
conio.walletService.walletActivities(params: params).asCallback { result in
    switch result {
    case .success(let activities):
        // WalletActivities
    case .failure(let error):
        // Operation Error
    }
}
```

## Dettaglio di un movimento

Recuperata la lista delle attività è possibile ottenere ulteriori informazioni su un *Activity* specifica richiedendone il dettaglio.

### Metodo

`walletService.activityDetails`

### Parametri

Un oggetto di tipo `ActivityDetailsParams` contenente:

- **activityId**: di tipo `String`, l'id dell'*Activity* della quale si vuole leggere il dettaglio;

- **currency**: di tipo `Currency`, la valuta nella quale si vuole conoscere il valore della transazioni di acquisto e vendita (attualmente solo Euro);

### Risposta

Un oggetto di tipo `ActivityDetails` contenente:

- **activityId**: di tipo `String`, l'id dell'attività;

- **type**: di tipo `ActivityType`, la tipologia di *Activity* (`SEND`, `BUY`, `SELL`, `RECEIVE`);

- **createdAt**: di tipo `Long`, l'istante temporale in cui è stata creata l'*Activity*, espresso come Unix Timestamp in millisecondi.

- **@Opzionale transaction**: di tipo `Transaction`, la transazione annessa. Popolato nel caso in cui sia stata effettuata una transazione. Contiene informazioni sulla transazione Bitcoin associata all'*Activity*, quali:

    - **hash**: di tipo `String`, l'hash della transazione Bitcoin;

    - **status**: di tipo `TransactionStatus`, lo stato di conferma della transazione Bitcoin legata all'*Activity* (`UNCONFIRMED`, `PARTIALLY_CONFIRMED`, `CONFIRMED`);

    - **type**: di tipo `TransactionType`, il tipo di transazione Bitcoin (`GENERIC` o `REDEPOSIT`, ovvero una transazione verso se stessi);

    - **addresses**: di tipo `List<String>`, gli indirizzi Bitcoin dei dei **mittenti** (per le transazioni in entrata) o **dei destinatari** (per le transazioni in uscita);

    - **cryptoAmount**: di tipo `long`

    - **miningFees**: di tipo `long`, le commissioni pagate alle rete Bitcoin per processare la transazione;

    - **isIncoming**: di tipo `booleano`, flag indicante se la transazione è in entrata o in uscita rispetto al portafoglio dell'utente;

    - **isLocal**: di tipo `booleano`, flag indicante se la transazione è stata ricevuta/inviata da/a un portafoglio Conio.

- **@Opzionale associatedBid**: l'offerta di acquisto annessa. Popolato in caso di attività di acquisto. Contiene le informazioni sulla richiesta di acquisto, quali:

    - **status**: di tipo `BidStatus`, lo stato del pagamento della richiesta di acquisto (`PAID`, `CHARGED`);

    - **cryptoAmount**: di tipo `long`, l'ammontare in **satoshi** (1 bitcoin = 100.000.000 satoshi) acquistato;

    - **fiatAmount**: di tipo `Decimal` (iOS) / `BigDecimal` (Android), il controvalore (rispetto al **cryptoAmount**) accordato per l'acquisto dei bitcoin, calcolato nella valuta indicata dal campo **currency**;

    - **serviceFee**: di tipo `Decimal` (iOS) / `BigDecimal` (Android), le commissioni pagate per la fruizione del servizio, calcolato nella valuta indicata dal campo **currency**;

    - **currency**: di tipo `Currency`, la valuta usata per l'acquisto dei bitcoin;

    - **paymentMethodId**: di tipo `String`, l'identificativo del metodo di pagamento;

    - **createdAt**: di tipo `long`, l'istante temporale in cui è stata creata l'*Activity*, espresso come Unix Timestamp in millisecondi;

    - **paidAt**: di tipo `long`, l'istante temporale in cui è stato effettuato il pagamento per l'acquisto dei bitcoin, espresso come Unix Timestamp in millisecondi;

    - **@Opzionale chargedAt**: di tipo `long`, l'istante temporale in cui è stata invaita la transazione bitcoin, espresso come Unix Timestamp in millisecondi. Nullo nel caso in cui la transazione non sia ancora stata effettuata.

- **@Opzionale associatedAsk**: l'offerta di vendita annessa. Popolato in caso di attività di vendita, Contiene le informazioni sulla richeista di vendita, quali:

    - **status**: di tipo `AskStatus`, lo stato del pagamento della richiesta di vendita (`CHARGED`, `PAID`)

    - **cryptoAmount**: di tipo `long`, l'ammontare in **satoshi** (1 bitcoin = 100.000.000 satoshi) venduto;

    - **fiatAmount**: di tipo `Decimal` (iOS) / `BigDecimal` (Android), il controvalore (rispetto al **cryptoAmount**) accordato per la vendita dei bitcoin, calcolato nella valuta indicata dal campo **currency**;

    - **serviceFee**: di tipo `Decimal` (iOS) / `BigDecimal` (Android), le commissioni pagate per la fruizione del servizio, calcolato nella valuta indicata dal campo **currency**;

    - **currency**: di tipo `Currency`, la valuta usata per la vendita dei bitcoin;

    - **sellMethodId**: di tipo `String`, l'identificativo del metodo di riscossione della vendita;

    - **cro**: di tipo `String`, il Codice Riferimento Operazione della transazione bancaria;

    - **iban**: di tipo `String`, l'IBAN del richiedente del bonifico bancario;

    - **createdAt**: di tipo `long`, l'istante temporale in cui è stata creata l'*Activity*, espresso come Unix Timestamp in millisecondi;

    - **chargedAt**: di tipo `long`, l'istante temporale in cui è stata invaita la transazione bitcoin, espresso come Unix Timestamp in millisecondi;

    - **@Opzionale paidAt**: di tipo `long`, l'istante temporale in cui è stato effettuato il pagamento per la vendita dei bitcoin, espresso come Unix Timestamp in millisecondi. Nullo nel caso in cui la transazione non sia ancora stata effettuata.

### Errori

- [Non autorizzato](../operation/Operation.md#Non-autorizzato)

### Codice

#### Android

```java
ActivityDetailsParams params = new ActivityDetailsParams("activityId", Currency.EUR);

conio.walletService.activityDetails(params)
    .asCallback(result -> result.analysis(
        details -> { /* Handle ActivityDetails */ },
        error -> { /* ... */ }
    ));
```

#### iOS

```swift
let params = ActivityDetailsParams(activityId: "activityId", currency: .eur)

conio.walletService.activityDetails(params: params).asCallback { result in
    switch result {
    case .success(let details):
        // ActivityDetails
    case .failure(let error):
        // Operation Error
    }
}
```

## Bilancio del portafoglio

Permette di recuperare il bilancio del portafoglio Bitcoin dell'utente.

### Metodo

`walletService.walletBalances`

### Risposta

Un oggetto di tipo `WalletBalances` contenente il valore di bitcoin presente nel wallet espresso in **satoshi** (1 bitcoin = 100.000.000 satoshi). Il valore si divide in:

- **confirmedBalance**: di tipo `long`, valore con almeno 3 conferme sulla blockchain Bitcoin e quindi disponibile per l'utente;

- **unconfirmedBalance**: di tipo `long`, valore con meno di 3 conferme e quindi non ancora disponibile.

### Errori

- [Non autorizzato](../operation/Operation.md#Non-autorizzato)

### Codice

#### Android

```java
conio.walletService.walletBalances()
    .asCallback(result -> result.analysis(
        balances -> { /* Handle WalletBalances */ },
        error -> { /* ... */ }
    ));
```

#### iOS

```swift
conio.walletService.walletBalances().asCallback { result in
    switch result {
    case .success(let balances):
        // WalletBalances
    case .failure(let error):
        // Operation Error
    }
}
```

## Codice di recupero Bitcoin

Permette di recuperare dalla memoria del dispositivo il "Codie di recupero Bitcoin": 12 parole di backup del portafoglio Bitcoin.

### Risposta

Un oggetto di tipo `MnemonicWords` contenente un array di 12 stringhe.

### Errori

- [Non autorizzato](../operation/Operation.md#Non-autorizzato)

### Codice

#### Android

```java
conio.walletService.readMnemonic()
    .asCallback(result -> result.analysis(
        mnemonic -> { /* Handle MnemonicWords */ },
        error -> { /* ... */ }
    ));
```

#### iOS

```swift
conio.walletService.readMnemonic().asCallback { result in
    switch result {
    case .success(let mnemonic):
        // MnemonicWords
    case .failure(let error):
        // Operation Error
    }
}
```
