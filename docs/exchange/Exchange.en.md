# Exchange operations

## Current Bitcoin Price

You can get the current buy or sell Bitcoin price.
The SDK can also give you the Bitcoin equivalent for a set amount of currency.

### Parameters

An object of type `CurrentPriceParams`:

- **currency**: which fiat currency (EUR) you want to have the exchange rate for.
- **@Optional amount**: the amount of Fiat currency (EUR) that you want to know the equivalent in BTC

### Returns

A `CurrentPrice` object:

- **buyPrice**: Buy exchange rate
- **sellPrice**: Sell exchange rate
- **timestamp**: price timestamp

### Code

#### Android

```java
// Current price
CurrentPriceParams params = new CurrentPriceParams(Currency.EUR);

// Conversion of 50.000.000 satoshi (0,5 BTC) in euro
CurrentPriceParams params = new CurrentPriceParams(Currency.EUR, 50_000_000L)

conio.exchangeService.currentPrice(params, result->{
  result.analysis(price-> {
    // CurrentPrice
  }, error-> {
     // Exception
  });
});
```

#### iOS
```swift
// Current price
let params = CurrentPriceParams(currency: .eur)

// Conversion of 50.000.000 satoshi (0,5 BTC) in euro
let params = CurrentPriceParams(currency: .eur, satoshiAmount: 50_000_000)

conio.exchangeService.currentPrice(params: params) { result in
 result.analysis(ifSuccess: { prices in
      // CurrentPrice
    }, ifFailure: { error in
      // ServiceError
    })
});
```

## Bitcoin hystorical price

You can get the Bitcoin hystorical price during a set amount of time.

### Parameters

An object `HistoricalPriceParams`:

- **currency**: which fiat currency you want to have the exchange rate for.
- **startTimestamp**: Initial timestamp.
- **endTimestamp**: Final timespamp.
- **@Optional interval**: Time between each price (week, day, hour...)

### Returns

Object `HistoricalPrices`:

* Contains a list of `CurrentPrice`
* An object `PriceAnalytics` containing:
  * **deltaFiat**: absolute exchange rate change during the selected period.
  * **deltaPercentage**: percentage change of the exchange rate during the selected period.
  * **trend**: enum: price increased, decreased or stayed the same.

### Code

#### Android

```java
// Price from April 16, 2019 to April 16, 2018
// Standard Interval: 1 day
HistoricalPriceParams params = new HistoricalPriceParams(
  Currency.EUR, 
  1523885446000L, 
  1563465540000L
);

// Price from April 16, 2019 to April 16, 2018
// Selected Interval: 1 week
HistoricalPriceParams params = new HistoricalPriceParams(
  Currency.EUR, 
  1523885446000L, 
  1563465540000L,
  604800000
);

conio.exchangeService.historicalPrices(params, result->{
  result.analysis(prices-> {
    // HistoricalPrices
  }, error-> {
    // Exception
  });
});
```

#### iOS
```swift
// Price from April 16, 2019 to April 16, 2018
// Standard Interval: 1 day
let params = HistoricalPriceParams(currency: .eur, startTimestamp: 1523885446000, endTimestamp: 1563465540000)

// Price from April 16, 2019 to April 16, 2018
// Selected Interval: 1 week
let params = HistoricalPriceParams(currency: .eur, startTimestamp: 1523885446000, endTimestamp: 1563465540000, interval: 604800000)

conio.exchangeService.historicalPrices(params: params) { result in
 result.analysis(ifSuccess: { prices in
      // HistoricalPrices
    }, ifFailure: { error in
      // ServiceError
    })
});
```

## Trading limits

Request user trading limits (assigned at signup)

### Returns

An object `AllTradingLimits (Android)` or `Limits (iOS)` containing:

- Two objects: `TradingLimits`, one for buying limits and one for selling limits. Inside of it we get:

    - **currentLimit**: current limit
    - **limits**: a list containing each limit (daily, monthly, yearly) and their maximum values.
    - **currentLimitsByType**: current limit for each of the limits.

- **minimumBuyAmount**: minimum amount in fiat currency (EUR) required to buy Bitcoin
- **minimumSellAmount**: minimum amount in fiat currency (EUR) required to sell Bitcoin

### Codice

#### Android

```java
conio.exchangeService.tradingLimits(result -> {
  result.analysis(limits -> {
    // TradingLimits
  }, error -> {
    // Exception
  });
});
```

#### iOS
```swift
conio.exchangeService.tradingLimits { result in
 result.analysis(ifSuccess: { limits in
      // TradingLimits
    }, ifFailure: { error in
      // ServiceError
    })
});
```

## Buy Bitcoin

In order to buy Bitcoin you will have to perform 2 operations. The first one creates a `Bid` (a request to buy some BTC at some price). Inside the created `Bid` you will find the `WiretransferInfo` that you will use to make the wire transfer necessary to pay for the Bitcoin. Once the wire transfer is completed you can perfom the second operation that will inform Conio that you payed the `Bid` by sending over a `CryptoProof`, required to proof the validity of the transaction.

## Bid creation

You can create a `RequestBid` with a **currency** (BTC or EUR) and an amount, expressed either in satoshi, or in Fiat currency. 
For example you can create a `RequestBid` in Euro to buy an amount in Bitcoin for the equivalent of 20€, or a `RequestBid` in Euro to buy 100.000.000 satoshi. 

If the request will be successful you will get a `Bid` containing an `ID`. With this identifier you will be able to **update** the Bid to get fresh info about it. This will be necessary if the user takes some time (more than 2 minutes) from the Bid request to the actual payment.

### Parameters

- **(Optional) id**: Bid id, insert only if you need to refresh the bid
- **(one of) satoshi**: amount of Bitcoin that the user wants to buy
- **(one of) fiatAmount**: amount of Fiat currency the user wants to spend to buy an equivalent Bitcoin amount
- **currency**: Fiat currency used to buy (EUR)

The SDK will allow you to insert only one of **satoshi** or **fiatAmount**. You should never input both of them at the same time.

### Returns

An object `CreatedBid` containing:

- **id**: identifier required to refresh or finalize a bid
- **currency**: Fiat currency used to buy (EUR)
- **satoshi**: Satoshi amount of the request
- **fiatAmount**: Fiat amount (EUR) of the request 
- **serviceFees**: Fees for the transaction in the selected **currency** 
- **expiration**: Bid expiration timestamp. If expired please refresh the Bid.
- **wiretransferInfo**: necessary info to pay for the bid

### Code

#### Android

```java

// Buy request for 100€
CreateOrRefreshBidParams params = 
  new CreateOrRefreshBidParams(Currency.EUR, 100d);

// Buy request for 1.000.000 satoshi
CreateOrRefreshBidParams params = 
  new CreateOrRefreshBidParams(Currency.EUR, 100000000l);

// Bid refresh for 100€
CreateOrRefreshBidParams params = 
  new CreateOrRefreshBidParams(
    "bididentifier", 
    Currency.EUR, 
    100d
  );

conio.exchangeService.createOrRefreshBid(params, result -> {
  result.analysis(bid -> {
    // CreatedBid
  }, error -> {
    // Exception
  });
});
```

#### iOS
```swift
// Buy request for 50€
let params = CreateOrRefreshBidParams(currency: .eur, fiatAmount: 50.0)

// Buy request for 1.000.000 satoshi
 let params = CreateOrRefreshBidParams(currency: .eur, satoshi: 1000000)
 
// Bid refresh for 100€
let params = CreateOrRefreshBidParams(bidID: "bididentifier", currency: .eur, fiatAmount: 100.0)

conio.exchangeService.createOrRefreshBid(params: params) { result in
 result.analysis(ifSuccess: { createdBid in
        // CreatedBid
    }, ifFailure: { error in
        // ServiceError
    })
});
```

## Bid Payment 

Once you have payed the `Bid` you can use the `Purchase` operation to receive the Bitcoin. You will have to submit a `CryptoProof`, that you can create in the same way as the one created during the signup. The only difference is the following DATA to concatenate (exactly in this order):

```
[proofID, "PAY_FOR_BID_WT", bidID, userID, Expiration]
```

### Parameters

An object `PurchaseParams` containing:

- **bidId**: `Bid` identifier referring to the bid you want to finalize
- **cryptoRequest**: a `BidCryptoRequest` 

### Returns

An object `PurchaseResult` containing:

- **bidId**: `Bid` identifier

### Errors

* INVALID_CRYPTO_PROOF Crypto proof is not valid
* INVALID_PAYMENT_METHOD Payment method is not valid
* UNSUPPORTED_PAYMENT_METHOD Payment method is not supported
* TRADING_LIMITS_EXCEEDED Bid exceed the maximum buy limit of the user
* TRADE_EXPIRED Bid is expired
* BID_ALREADY_PAID Bid was already paid
* BID_NOT_YET_PAID Bid has not been paid yet
* UNRECOVERABLE_BID Bid is in an error state
* FIAT_AMOUNT_TOO_LOW Fiat amount is lower than minimum limit

### Code

#### Android

```java
BidCryptoRequest bidCryptoRequest = 
  createCryptoRequest() // Your implementation

PurchaseParams params = 
  new PurchaseParams("bidId", bidCryptoRequest, card);

conio.exchangeService.purchase(params, result -> {
  result.analysis(bid -> {
    // PurchaseResult
  }, error -> {
    // Exception
  });
});
```

#### iOS
```swift
let cryptoRequest = createCryptoRequest() // Your implementation

let params = PurchaseParams(bidID: "bidID", paymentCard: card, cryptoRequest: cryptoRequest)

conio.exchangeService.purchase(params: params) { result in
 result.analysis(ifSuccess: { bid in
    // PurchaseResult
    }, ifFailure: { error in
    // ServiceError
    })
});
```

## Sell Bitcoin
In order to buy Bitcoin you will have to perform 2 operations. The first one creates a `Ask` (a request to sell some BTC at some price). The second one will pay said `Ask`, by using the ask identifier.  The SDK will sign the Bitcoin transaction that moves the bitcoins from the user wallet, returning the id of said completed Ask.

## Ask Creation
You can create a `CreatedAsk` in Euro to sell an amount in Bitcoin for the equivalent of 50€, or a `CreatedAsk` in Euro to sell 100.000.000 satoshi. 

The request will return an `Ask` containing an `ID`. With this identifier you will be able to **update** the Ask to get fresh info about it. This will be necessary if the user takes some time (more than 2 minutes) from the Ask request to the actual sell.
### Parameters

- **(Optional) id**: Ask id, insert only if you need to refresh the Ask
- **(one of) satoshi**: bitcoin amount the user wants to sell 
- **(one of) fiatAmount**: amount of Fiat currency the user wants to receive when selling Bitcoin 
- **currency**: Fiat currency to receive (EUR) 

The SDK will allow you to insert only one of **satoshi** or **fiatAmount**. You should never input both of them at the same time.

### Returns

An object `CreatedAsk` containing:

- **id**: identifier required to refresh or finalize a ask
- **currency**: Fiat currency to receive (EUR)
- **satoshi**: Satoshi amount of the request
- **fiatAmount**: Fiat amount (EUR) of the request 
- **serviceFees**: Fees for the transaction in the selected **currency** 
- **expiration**: Ask expiration timestamp. If expired please refresh the Ask.
- **minerFees**: Bitcoin network fees, used to pay for the inclusion of the transaction in the blockchain.

### Errors

* TRADING_LIMITS_EXCEEDED 
* NOT_ENOUGH_BTC_AMOUNT 
* NO_SUCH_SELLER (Internal selling error)
* NO_SUCH_WALLET (Internal wallet error)

#### iOS
```swift

// Sell request for 50€
let params = 
  CreateOrRefreshAskParams(currency: .eur, fiatAmount: 50.0)

// Sell request for 100000000 satoshi
let params = 
  CreateOrRefreshAskParams(currency: .eur, satoshi: 100000000)

// Refresh ask 
let params = 
  CreateOrRefreshAskParams(askID: "id", currency: .eur, fiatAmount: 100.0)

conio.exchangeService.createOrRefreshAsk(params: params) { result in
  result.analysis(ifSuccess: { createdAsk in
    // CreatedBid
  }, ifFailure: { error in
    // ServiceError
  })
}
```

#### Android
```java

// Sell request for 50€
CreateOrRefreshAskParams params = 
  new CreateOrRefreshAskParams(Currency.EUR, 50d);

// Refresh ask 
CreateOrRefreshAskParams params = 
  new CreateOrRefreshAskParams("id", Currency.EUR, 50d);

conio.exchangeService.createOrRefreshAsk(params: params) { result in
 result.analysis(ifSuccess: { createdAsk in
        // CreatedAsk
    }, ifFailure: { error in
        // Exception
    })
});
```

## Finalize Ask 

To finalize the sell you just need to input the ID of the `CreatedAsk` in the `Sell` operation.
### Parameters

An object `SellParams` containing:

- **askId**: `Ask` identifier

### Returns

An object `SellResult` containing:

- **askId**: `Ask` identifier
### Errors

* TRADING_LIMITS_EXCEEDED 
* TRADE_EXPIRED 
* UNRECOVERABLE_ASK 
* ASK_ALREADY_PAID 
* NOT_ENOUGH_BTC_AMOUNT_E 
* DUST_ASK (Bitcoin amount is too low)
* FIAT_AMOUNT_TOO_LOW 

### Code

#### iOS

```swift
let params = SellParams(askID: askID)

conio.exchangeService.sell(params: params) { result in
  result.analysis(ifSuccess: { sellResult in
    // SellResult
  }, ifFailure: { error in
    // ServiceError
  })
}
```

#### Android

```java
SellParams sellParams = new SellParams("askId");

conio.exchangeService.sell(params: params) { result in
 result.analysis(ifSuccess: { sellResult in
        // SellResult
    }, ifFailure: { error in
        // Exception
    })
});
```

## Get available trading reports

This operation retrieves the list of trading report periods available for the Conio user. Each period is represented by a `TradingReportPeriod` object, which specifies the fiscal year and, optionally, the relevant quarter.

The `year` field may be nil when the report refers to the previous fiscal year, while the `quarter` field may be nil when the report covers the entire fiscal year. If specified, the quarter identifies one of the four periods of the year: first quarter (`Q1`), second quarter (`Q2`), third quarter (`Q3`), or fourth quarter (`Q4`).

### Method

`exchangeService.getAvailableTradingReports`

### Response

An object of type `AvailableTradingReportsResult`, containing the reportPeriods list of available reporting periods. Each item is a `TradingReportPeriod` object consisting of:
- `year`: the fiscal year of the report, represented as a string. It is nil if the report refers to the previous fiscal year.
- `quarter`: the reporting quarter, represented by a value of the TradingReportPeriod.Quarter enumeration. It is nil if the report covers the entire fiscal year. The possible values for quarter are:
    - `q1`: first quarter, from January 1 to March 31.
    - `q2`: second quarter, from April 1 to June 30.
    - `q3`: third quarter, from July 1 to September 30.
    - `q4`: fourth quarter, from October 1 to December 31.

### Code

#### Android

```java
conio.exchangeService.getAvailableTradingReports()
    .asCallback(result -> result.analysis(
        availableTradingReports -> { /* Handle AvailableTradingReportsResult */ },
        error -> { /* ... */ }
    ));
```


#### iOS

```swift
conio.exchangeService.getAvailableTradingReports().asCallback { result in
    switch result {
    case .success(let availableTradingReports):
        // Handle AvailableTradingReportsResult
    case .failure(let error):
        // Operation Error
    }
}
```

## Download a specific financial report

This operation allows the user to request and download a financial report for a specific fiscal period. The period is specified through a `TradingReportPeriod` object, which identifies the fiscal year and, optionally, the relevant quarter.

The request parameters are defined through the `YearlyReportParametable` protocol, which is implemented by the `FinancialReportParams` structure.

### Method

`exchangeService.financialReport`

### Parameters

An object conforming to the `YearlyReportParametable` protocol, such as `FinancialReportParams`, containing:
- `period`: a `TradingReportPeriod` object identifying the reporting period to download, specifying the fiscal year and, optionally, the quarter.

### Response

A `ServiceConsumer<Data>` that allows the outcome of the operation to be read. Upon success, it returns the downloaded financial report data as a `Data` object.

### Code

#### Android

```java
FinancialReportParams params = new FinancialReportParams(period);

conio.userService.financialReport(params)
    .asCallback(result -> result.analysis(
        data -> { /* Handle Data */ },
        error -> { /* ... */ }
    ));
```

#### iOS

```swift
let params = FinancialReportParams(pediod: ...)

conio.userService.financialReport(with: params).asCallback { result in
    switch result {
    case .success(let data):
        // Handle Data
    case .failure(let error):
        // Operation Error
    }
}
```
