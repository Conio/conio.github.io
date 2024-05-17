# Operazioni sul mercato

## Prezzo attuale del Bitcoin

È possibile recuperare il miglior prezzo di acquisto e di vendita attuale del bitcoin, specificando la valuta nel quale lo si vuole ottenere. Inoltre, l'SDK offre la possibilità di convertire un ammontare in bitcoin nella valuta specificata.

### Metodo

`exchangeService.currentPrice`

### Parametri

Un oggetto di tipo `CurrentPriceParams` contenente:

- **currency**: di tipo `Currency`, la valuta in cui si vuole ottenere il prezzo;

- **@Opzionale cryptoAmount**: di tipo `long`, l'ammontare in **satoshi** (1 bitcoin = 100.000.000 satoshi) che si vuole convertire nella valuta indicata.

### Risposta

Un `CurrentPrice` contenente:

- **buyFiatAmount**: di tipo `Decimal` (iOS) / `BigDecimal` (Android), il prezzo di acquisto, calcolato nella valuta indicata tramite il campo **currency**;

- **sellFiatAmount**: di tipo `Decimal` (iOS) / `BigDecimal` (Android), il prezzo di vendita, calcolato nella valuta indicata tramite il campo **currency**.

### Codice

#### Android

```java
// Example 1: get current price
CurrentPriceParams params = new CurrentPriceParams(Currency.EUR);

// Example 2: get current price of a specified amount
CurrentPriceParams params = new CurrentPriceParams(Currency.EUR, 100000000);

conio.exchangeService.currentPrice(params)
    .asCallback(result -> result.analysis(
        currentPrice -> { /* Handle CurrentPrice */ },
        error -> { /* ... */ }
    ));
```

#### iOS
```swift
// Recupero del prezzo attuale
let params = CurrentPriceParams(currency: .eur)

// Conversione di 50.000.000 satoshi (0,5 BTC) in euro
let params = CurrentPriceParams(currency: .eur, satoshiAmount: 50_000_000)

let consumer = conio.exchangeService.currentPrice(params: params)
consumer.asCallback { result in
    switch result {
    case .success(let prices):
        // CurrentPrice
    case .failure(let error):
        // Operation Error
    }
}
```

## Prezzo storico del Bitcoin

È possibile recuperare il prezzo storico del Bitcoin selezionando una finestra temporale di riferimento.

### Metodo

`exchangeService.historicalPrices`

### Parametri

Un oggetto di tipo `HistoricalPricesParams` contenente:

- **currency**: di tipo `Currency`, la valuta in cui si vuole ottenere il prezzo;

- **timeFrame**: di tipo `TimeFrame`, la finestra temporale di riferimento;

- **@Default(24h) interval**: di tipo `long`, l'intervallo che si vuole porre tra i prezzi restituiti;

### Risposta

Un `HistoricalPrices` contenente:

* **prices**: di tipo `List<PricePoint>`, la lista dei prezzi del bitcoin nella finestra temporale specificata;

* **analytics**: di tipo `PriceAnalytics`, contenente:

    * **deltaFiat**: di tipo `Decimal` (iOS) / `BigDecimal` (Android), la variazione in valuta del prezzo del Bitcoin dall'inizio del periodo di riferimento;

    * **deltaPercentage**: la variazione in percentuale del prezzo del Bitcoin dall'inizio del periodo di riferimento;

    * **trend**: di tipo `PriceTrend`, un enumerato che rappresenta se il prezzo del Bitcoin, dall'inizio del periodo di riferimento, è cresciuto, è diminuito o è rimasto stagnante;

### Codice

#### Android

```java
// Example 1: get last month prices with default interval (1 day)
HistoricalPricesParams params = new HistoricalPricesParams(
    Currency.EUR,
    TimeFrame.lastMonth()
);

// Example 2: get prices from 16th April 2018 to 16th April 2019 with 1 week interval
HistoricalPricesParams params = new HistoricalPricesParams(
    Currency.EUR,
    new TimeFrame(1523885446000L, 1563465540000L),
    604800000
);

conio.exchangeService.historicalPrices(params)
    .asCallback(result -> result.analysis(
        prices -> { /* Handle HistoricalPrices */ },
        error -> { /* ... */ }
    ));
```

#### iOS

```swift
// Prezzo dal 16 aprile 2019 al 16 aprile 2018
// Intervallo standard: 1 giorno
let params = HistoricalPriceParams(currency: .eur, startTimestamp: 1523885446000, endTimestamp: 1563465540000)

// Prezzo dal 16 aprile 2019 al 16 aprile 2018
// Intervallo selezionato: 1 settimana
let params = HistoricalPriceParams(currency: .eur, startTimestamp: 1523885446000, endTimestamp: 1563465540000, interval: 604800000)

let consumer = conio.exchangeService.historicalPrices(params: params)
consumer.asCallback { result in
    switch result {
    case .success(let prices):
        // HistoricalPrices
    case .failure(let error):
        // Operation Error
    }
}
```


## Recupero informazioni di trading

Recupero delle informazioni riassuntive delle operazioni di compravendita eseguite dall'utente.

### Metodo

`exchangeService.tradingInfo`

### Parametri

Un oggetto di tipo `TradingInfoParams`, contenente:

- **currency**: di tipo `Currency`, la valuta sulla quale si vuole ottenere la risposta;

### Risposta

- **weightedBidBalance**: di tipo `Decimal` (iOS) / `BigDecimal` (Android), controvalore investito, calcolato come la media pesata del valore (in valuta fiat) degli acquisti moltiplicato per il bilancio attuale;

- **currency**: di tipo `Currency`, la valuta di riferimento della risposta;

- **bidSummary**: di tipo `TradingSummary`, contenente un riepilogo delle operazioni di acquisto;

- **askSummary**: di tipo `TradingSummary`, contenente un riepilogo delle operazioni di vendita;

Le proprietà di tipo `TradingSummary` contengono:

- **operationsCount**: di tipo `intero`, il numero totale di operazioni;

- **totalFiatAmount**: di tipo `Decimal` (iOS) / `BigDecimal` (Android), l'ammontare totale delle operazioni.

### Codice

#### Android

```java
TradingInfoParams params = new TradingInfoParams(Currency.EUR);

conio.exchangeService.tradingInfo(params)
    .asCallback(result -> result.analysis(
        info -> { /* Handle TradingInfo */ },
        error -> { /* ... */ }
    ));
```

```swift

let consumer = conio.exchangeService.tradingInfo()
consumer.asCallback { result in
    switch result {
    case .success(let info):
        // Handle TradingInfo
    case .failure(let error):
        // Operation Error
    }
}
```

## Recupero commissioni di trading

Per recuperare le informazioni delle commissioni sulle operazioni di compravendita.

### Metodo

`exchangeService.tradingFees`

### Parametri

Un oggetto di tipo `TradingFeesParams`, contenente:

- **currency**: di tipo `Currency`, la valuta sulla quale si vuole ottenere la risposta;

### Risposta

Un oggetto di tipo `TradingFees`, contenente:

- **currency**: di tipo `Currency`, la valuta di riferimento della risposta;

- **bidServiceFees**: di tipo `List<ServiceFee>`, contenente la lista delle fascie di commissioni per le operazioni di acquisto;

- **askServiceFees**: di tipo `List<ServiceFee>`, contenente la lista delle fascie di commissioni per le operazioni di vendita.

Le proprietà di tipo `ServiceFee` contengono:

- **rangeFrom**: di tipo `Decimal` (iOS) / `BigDecimal` (Android), il valore (in valuta fiat) dal quale viene applicata;

- **@Opzionale percentage**: di tipo `double`, la percentuale di commissione rispetto al valore del operazione, nulla se la `ServiceFee` rappresenta una commissione assoluta;

- **@Opzionale fiatAmount**: di tipo `Decimal` (iOS) /`BigDecimal` (Android), la commisione assuluta applicata su ogni operazione, nulla se la `ServiceFee` rappresenta una commissione in percentuale.

### Codice

#### Android

```java
TradingFeesParams params = new TradingFeesParams(Currency.EUR);

conio.exchangeService.tradingFees(params)
    .asCallback(result -> result.analysis(
        fees -> { /* Handle TradingFees */ },
        error -> { /* ... */ }
    ));
```

```swift
let consumer = conio.exchangeService.tradingFees()
consumer.asCallback { result in
    switch result {
    case .success(let fees):
        // Handle TradingFees
    case .failure(let error):
        // Operation Error
    }
}
```

## Recupero limiti di trading

Per recuperare i limiti di compravendita associati ad un utente, assegnati in fase di signup tramite il campo **userLevel**.

### Metodo

`exchangeService.tradingLimits`

### Risposta

Un oggetto di tipo `AllTradingLimits`, contenente:

- **buyLimits**: di tipo `TradingLimits`, contenenti informazioni sui limiti di acquisto;

- **sellLimits**: di tipo `TradingLimits`, contenenti informazioni sui limiti di vendita.

Le proprietà di tipo `TradingLimits` contengono:

- **minFiatAmount**: di tipo `Decimal` (iOS) / `BigDecimal` (Android), il limite minimo attualmente a disposizione;

- **maxFiatAmount**: di tipo `Decimal` (iOS) / `BigDecimal` (Android), il limite massimo attualmente a disposizione;

- **allLimits**: di tipo `List<Limit>`, una lista di limiti, ciascuno conterrà la rispettiva tipologia (`DAILY`, `MONTHLY`, `YEARLY`) ed il valore per ciascuno di essi;

- **currentLimits**: di tipo `List<Limit>`, il valore residuo per ciascuno dei limiti contenuti nell'oggetto `allLimits` del punto precedente.

### Codice

#### Android

```java
conio.exchangeService.tradingLimits()
    .asCallback(result -> result.analysis(
        limits -> { /* Handle AllTradingLimits */ },
        error -> { /* ... */ }
    ));
```

#### iOS
```swift
let consumer = conio.exchangeService.tradingLimits()
consumer.asCallback { result in
    switch result {
    case .success(let fees):
        // Handle AllTradingLimits
    case .failure(let error):
        // Operation Error
    }
}
```


## Acquisto di Bitcoin

Per poter acquistare dei Bitcoin è necessario effettuare due operazioni. La prima è quella di creazione di una `Bid`, ovvero di una richiesta di acquisto di una determinata somma di Bitcoin ad un certo prezzo. All'interno della `Bid` si troveranno le `WiretransferInfo` che dovranno essere usate dal client per effettuare il pagamento. Infine si dovrà utilizzare la seconda operazione verso Conio per comunicare l'avvenuto pagamento della `Bid` allegando anche una [`BidCryptoRequest`](../operation/CryptoRequest.md#creazione-bidcryptorequest), generata client side, per testimoniare la legittimità dell'operazione.

## Creazione della Bid

Una `Bid` si crea specificando la **valuta** che si intende utilizzare per la transazione e l'importo, o in satoshi o in valuta corrente. Ad esempio, sarà quindi possibile richiedere una `Bid` per l'acquisto di 150€ di Bitcoin o una `Bid` per l'acquisto di 100.000.000 satoshi.

Una volta inviata la richiesta, si otterrà una `CreatedBid` contenente, tra le altre informazioni un `bidId`. Con questo identificativo sarà possibile **aggiornare** la richiesta di Bid per rimandarne la scadenza e per ottenere le informazioni sul tasso di cambio più aggiornate. Questo scenario è utile nei casi in cui tra la richiesta della Bid e l'effettiva azione dell'utente passi del tempo che renderebbe il tasso di cambio obsoleto.

### Metodo

`exchangeService.createOrRefreshBid`

### Parametri

Un oggetto di tipo `CreateOrRefreshBidParams`, costruibile tramite i metodi factory `CreateOrRefreshBidParams.fromFiat` o `CreateOrRefreshBidParams.fromCrypto` che richiedono:

- **currency**: di tipo `Currency`, la valuta dell'operazione;

- **amount**: di tipo `long` per `.fromCrypto` o `Decimal` (iOS) / `BigDecimal` (Android) per `.fromFiat`, l'ammontare, a seconda del metodo usato, in satoshi o nella valuta scelta che si vuole acquistare;

- **@Opzionale bidId**: di tipo `String`, l'id della bid, da valorizzare solo in caso di refresh della bid stessa.

### Risposta

Un oggetto di tipo `CreatedBid` che contiene:

- **id**: di tipo `String`, l'id utile al refresh o alla finalizzazione della bid;

- **currency**: di tipo `Currency`, la valuta dell'operazione;

- **cryptoAmount**: di tipo `long`, l'ammontare in satoshi della richiesta d'acquisto;

- **fiatAmount**: di tipo `Decimal` (iOS) / `BigDecimal` (Android), l'ammontare in valuta corrente della richiesta d'acquisto al netto delle commissioni;

- **grossFiatAmount**: di tipo `Decimal` (iOS) / `BigDecimal` (Android), l'ammontare in valuta corrente della richiesta d'acquisto comprensivo delle commissioni;

- **serviceFee**: di tipo `Decimal` (iOS) / `BigDecimal` (Android), le commissioni di servizio per la transazione, espresse nella **currency** di riferimento

- **expiration**: di tipo `long`, il timestamp di scadenza della richiesta di pagamento. Se la bid scade sarà necessario aggiornarla per proseguire

- **wireTransferInfo**: di tipo `WireTransferInfo`, le informazioni necessarie per procedere al pagamento della Bid tramite bonifico.

### Codice

#### Android

```java
// Example 1: €200 bid
CreateOrRefreshBidParams params = CreateOrRefreshBidParams.fromFiat(Currency.EUR, 20000);
// Example 2: 1.000.000.000 satoshi bid
CreateOrRefreshBidParams params = CreateOrRefreshBidParams.fromCrypto(Currency.EUR, 1000000000);

conio.exchangeService.createOrRefreshBid(params)
    .asCallback(result -> result.analysis(
        bid -> { /* Handle CreatedBid */ },
        error -> { /* ... */ }
    ));
```


#### iOS
```swift

// Richiesta d'acquisto per 50€
let params = CreateOrRefreshBidParams(currency: .eur, fiatAmount: 50.0)

// Richiesta d'acquisto per 1.000.000 satoshi
 let params = CreateOrRefreshBidParams(currency: .eur, satoshi: 1000000)

// Aggiornamento di una richiesta d'acquisto per 100€
let params = CreateOrRefreshBidParams(bidID: "bididentifier", currency: .eur, fiatAmount: 100.0)

let consumer = conio.exchangeService.createOrRefreshBid(params: params)
consumer.asCallback { result in
    switch result {
    case .success(let bid):
        // Handle CreatedBid
    case .failure(let error):
        // Operation Error
    }
}
```

## Utilizzo della Bid (pagamento)

Una volta effettuato il pagamento tramite bonifico si dovrà usare l'operazione `purchase` per comunicare a Conio l'avvenuto pagamento. Questa operazione richiederà una [`BidCryptoRequest`](../operation/CryptoRequest.md#creazione-bidcryptorequest).

### Metodo

`exchangeService.purchase`

### Parametri

Un oggetto di tipo `PurchaseParams` contenente:

- **bidId**: d tipo `String`, l'id della `Bid` da pagare

- **cryptoRequest**: di tipo `BidCryptoRequest`, configurabile come [descritto nell'apposita sezione](../operation/CryptoRequest.md#creazione-bidcryptorequest)

### Risposta

Un oggetto di tipo `Success`, che conferma l'avvenuta operazione.

### Errori

* INVALID_CRYPTO_PROOF La crypto proof non è valida
* INVALID_PAYMENT_METHOD Il metodo di pagamento non è valido
* UNSUPPORTED_PAYMENT_METHOD Il metodo di pagamento non è supportato
* TRADING_LIMITS_EXCEEDED La bid viola i limiti massimi di acquisto dell'utente
* TRADE_EXPIRED La bid è scaduta
* BID_ALREADY_PAID La bid è già stata pagata
* BID_NOT_YET_PAID La bid non è ancora stata pagata
* UNRECOVERABLE_BID La bid è in errore
* FIAT_AMOUNT_TOO_LOW L'importo in Fiat è inferiore al limite minimo

### Codice

#### Android

```java
PurchaseParams params = new PurchaseParams("bidId", bidCryptoRequest);

conio.exchangeService.purchase(params)
    .asCallback(result -> result.analysis(
        success -> { /* Handle Success */ },
        error -> { /* ... */ }
    ));
```

#### iOS
```swift
let params = PurchaseParams(bidId: "bidId", cryptoRequest: bidCryptoRequest)
let consumer = conio.exchangeService.purchase(params: params)
consumer.asCallback { result in
    switch result {
    case .success:
        // Handle Success
    case .failure(let error):
        // Operation Error
    }
}
```


## Vendita di Bitcoin

Per poter vendere dei Bitcoin è necessario effettuare due operazioni. La prima è quella di creazione di una `Ask`, ovvero di una richiesta di vendita di una determinata somma di Bitcoin ad un certo prezzo. Si procede poi con il pagamento di tale `Ask`, passando l'`askId` e allegando anche una [`AskCryptoRequest`](../operation/CryptoRequest.md#creazione-askcryptorequest), generata client side, per testimoniare la legittimità dell'operazione. L'SDK firmerà la transazione che sposterà i Bitcoin dal wallet dell'utente, restituendo alla fine l'id della `Ask` completata.

## Creazione della Ask

Per richiedere una `Ask` si dovrà procedere analogamente a quanto visto per la Bid.
Sarà quindi possibile richiedere una `CreatedAsk` per la vendita di 150€ o una per la vendita di 100.000.000 satoshi.

Una volta inviata la richiesta, si otterrà una `CreatedAsk` contenente, tra le altre informazioni un `askId`. Con questo identificativo sarà possibile **aggiornare** la richiesta di Ask per rimandarne la scadenza e per ottenere le informazioni sul tasso di cambio più aggiornate. Questo scenario è utile nei casi in cui tra la richiesta della Ask e l'effettiva azione dell'utente passi del tempo che renderebbe il tasso di cambio obsoleto.

### Metodo

`exchangeService.createOrRefreshAsk`

### Parametri

Un oggetto di tipo `CreateOrRefreshAskParams`, costruibile tramite i metodi factory `CreateOrRefreshAskParams.fromFiat`, `CreateOrRefreshAskParams.fromCrypto` o `CreateOrRefreshAskParams.withAll` che richiedono:

- **currency**: di tipo `Currency`, la valuta dell'operazione;

- **@Opzionale cryptoAmount**: di tipo `long` per `.fromCrypto`, l'ammontare in satoshi che si vuole vendere;

- **@Opzionale fiatAmount**: di tipo `Decimal` (iOS) / `BigDecimal` (Android) per `.fromFiat`, l'ammontare nella valuta scelta che si vuole vendere;

- **@Opzionale askId**: di tipo `String`, l'id della ask, da valorizzare solo in caso di refresh della ask stessa.

Tramite il metodo factory `CreateOrRefreshAskParams.withAll` è possibile richiedere l'importo massimo vendibile. Tale importo sarà sogetto, oltre che alla disponibilità del utente, anche ai suoi limiti di vendita.

### Risposta

Un oggetto di tipo `CreatedAsk` che contiene:

- **askId**: di tipo `String`, l'id utile al refresh o alla finalizzazione della ask;

- **currency**: di tipo `Currency`, la valuta dell'operazione;

- **cryptoAmount**: di tipo `long`, l'ammontare in satoshi della richiesta d'acquisto

- **fiatAmount**: di tipo `Decimal` (iOS) / `BigDecimal` (Android), l'ammontare in valuta corrente della richiesta d'acquisto;

- **serviceFee**: di tipo `Decimal` (iOS) / `BigDecimal` (Android), le commissioni di servizio per la transazione, espresse nella **currency** di riferimento;

- **miningFee**: di tipo `long`, le commissioni per scrivere la transazione in blockchain, espresse in satoshi;

- **expiration**: di tipo `long`, lo Unix Timestamp di scadenza della richiesta di pagamento. Se la bid scade sarà necessario aggiornarla per proseguire

### Errori

* TRADING_LIMITS_EXCEEDED L'utente ha 0 Eur di limiti residui
* NOT_ENOUGH_BTC_AMOUNT solo se non ha btc L'utente non ha alcun bitcoin
* NO_SUCH_SELLER Errore interno del sottosistema di vendita
* NO_SUCH_WALLET Errore interno del sottosistema di wallet


#### Android
```java
// Example 1: €200 ask
CreateOrRefreshAskParams params = CreateOrRefreshAskParams.fromFiat(Currency.EUR, BigDecimal("200"));
// Example 2: 1.000.000.000 satoshi ask
CreateOrRefreshAskParams params = CreateOrRefreshAskParams.fromCrypto(Currency.EUR, 1000000000);

conio.exchangeService.createOrRefreshAsk(params)
    .asCallback(result -> result.analysis(
        ask -> { /* Handle CreatedAsk */ },
        error -> { /* ... */ }
    ));
```

#### iOS
```swift

// Richiesta di vendita per 50€
let params =
    CreateOrRefreshAskParams(currency: .eur, fiatAmount: 50.0)

// Richiesta di vendita per 100000000 satoshi
let params =
    CreateOrRefreshAskParams(currency: .eur, satoshi: 100000000)

// Aggiornamento del valore di una Ask esistente
let params =
    CreateOrRefreshAskParams(askID: "id", currency: .eur, fiatAmount: 100.0)


conio.exchangeService.createOrRefreshAsk(params: params).asCallback { result in
    switch result {
    case .success(let createdAsk):
        // CreatedBid
    case .failure(let error):
        // Operation Error
    }
}
```


## Utilizzo della Ask

Ottenuta la `Ask` da utilizzare è possibile procedere con la finalizzazione della vendita. Per effettuare questa operazione bisognerà passare l'ID della `CreatedAsk` alla `Sell` operation, insieme alla [`AskCryptoRequest`](../operation/CryptoRequest.md#creazione-askcryptorequest).

### Metodo

`exchangeService.sell`

### Parametri

Un oggetto di tipo `SellParams` contenente:

- **askId**: di tipo `String`, l'id della `Ask`

- **cryptoRequest**: di tipo `AskCryptoRequest`, configurabile come [descritto nell'apposita sezione](../operation/CryptoRequest.md#creazione-askcryptorequest)

### Risposta

Un oggetto di tipo `Success` che conferma l'avvenuta operazione.


### Errori

* TRADING_LIMITS_EXCEEDED La ask viola i limiti massimi di acquisto dell'utente
* TRADE_EXPIRED La ask è scaduta
* UNRECOVERABLE_ASK La ask è in errore
* ASK_ALREADY_PAID La ask è già stata pagata
* NOT_ENOUGH_BTC_AMOUNT_E Bitcoin disponibili non sufficienti
* DUST_ASK Importo in Bitcoin troppo piccolo
* FIAT_AMOUNT_TOO_LOW Importo in Eur troppo basso

### Codice

#### Android

```java
SellParams params = new SellParams("askId", askCryptoRequest);

conio.exchangeService.sell(params)
    .asCallback(result -> result.analysis(
        success -> { /* Handle Success */ },
        error -> { /* ... */ }
    ));
```


#### iOS

```swift
let params = SellParams(askID: askID)

conio.exchangeService.createOrRefreshAsk(params: params).asCallback { result in
    switch result {
    case .success:
        // Handle Succes
    case .failure(let error):
        // Operation Error
    }
}
```
