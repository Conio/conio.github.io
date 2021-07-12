# Wallet operations

# Bitcoin address

Show one of the unused Bitcoin addresses of the wallet, that you can use to receive bitcoins.

## Returns

A `string` containing the Bitcoin address.

## Code

### Android

```java
conio.walletService.currentBitcoinAddress(result->{
    result.analysis(address-> {
        // String
    }, error-> {
        // Exception
    });
});
```

### iOS

```swift
conio.walletService.currentBitcoinAddress { result in   
    result.analysis(ifSuccess: { address in
        // String
    }, ifFailure: { error in
        // ServiceError
    })
}
```


# Bitcoin Movement List

Each transaction (send, receive, buy, sell) is represented by an `Activity`. You can get a list of these activites using the following method:

## Parameters

An `ActivitiesParams` struct containing:

- **index**: You can get 6 activities at a time. The index is the starting point of the list you want. For example using an index = 0 means you will get the last 6 activities. Then you can repeat this with index 6 which will get you the activities right before.
**important**: To get all the activities you just have to repeat this call until you get less than 6 activities.

- **types**: you can use types if you want to filter the activities. For example you want to get only the buy activities.

- **currency**: the fiat currency your activities will be priced in.

### Returns 
A `WalletActivities` struct containing:
-  **activities**: an array of `Activity`.
Each activity has its own `ID`, a `Type` (send, buy, sell, receive), an amount in `Satoshi`, and a `confirmationStatus` which will let you know if a bitcoin transaction is included in the blockchain.

## Code

### Android

```java
// To retrieve all the activities
ActivityType[] types = ActivityType.all()
ActivitiesParams params = new ActivitiesParams(0, types, Currency.EUR);

// To retrieve purchases and sells
ActivityType[] types = new ActivityType[] { 
    ActivityType.BUY, 
    ActivityType.SELL 
};

ActivitiesParams params = new ActivitiesParams(0, types, Currency.EUR);

conio.walletService.walletActivities(params, result->{
    result.analysis(activities-> {
        // WalletActivities
    }, error-> {
        // Exception
    });
});
```

### iOS

```swift

// To retrieve all the activities
let params = ActivitiesParams(
    index: 0, 
    types: ActivityType.all
    currency: .eur
)

// To retrieve only purchases and sells
let params = ActivitiesParams(
    index: 0, 
    types: [.buy, .sell]
    currency: .eur
)

conio.walletService.walletActivities(params: activitiesParams) { result in
    result.analysis(ifSuccess: { activities in
        // WalletActivities
    }, ifFailure: { error in
        // ServiceError
    })
}
```

# Activity detail

You can get all the info about a single activity by using this method. 


## Parameters

An `ActivityDetailsParams` containing:

- **activityId**: the identifier of the activity you want to get the details of.
- **currency**: the fiat currency your activity will be priced in.

## Returns

An `ActivityDetails` containing:

- **id**: identifier of the activity
- **type**: activity type
- **timestamp**: timestamp when the activity was created
- **@Optional transaction**: the info about the Bitcoin transaction related to that activity. Contains info like the hash of the transaction, number of confirmations, the Bitcoin address that is receiving the Bitcoin, the fiat currency equivalent, the fees payed and more.
- **@Optional bid**: info about the bid. Contains all the info about the purchase.
- **@Optional payment**: info about the payment, including the id of the payment method, the value of the payment and its status.
- **@Optional ask**: info about the ask. Contains all the info about the sell.
- **@Optional sell**: info about the wire transfer, the `identifier`, `cro` 

## Code

### Android

```java
ActivityDetailsParams params = new ActivityDetailsParams("id", Currency.EUR);    

conio.walletService.activityDetails(params, result->{
    result.analysis(details-> {
        // ActivityDetails
    }, error-> {
        // Exception
    });
});
```

### iOS

```swift
let params = ActivityDetailsParams(activityId: "activityId", currency: .eur)

 conio.walletService.activityDetails(params: params) { result in
    result.analysis(ifSuccess: { details in
        // ActivityDetails                 
    }, ifFailure: { error in
        // ServiceError               
    })
}
```

# Wallet balance
You can get the balance of the wallet.

## Returns 
A `WalletDetails` containing the amount of Bitcoin in the wallet (the amount is expressed in satoshi, the smallest unit of Bitcoin) (1 bitcoin = 100.000.000)

- **confirmedBalance**: bitcoins that have at least 3 confirmations on the blockchain and that the user can send/sell
- **unconfirmedBalance**: bitcoins with less than 3 confirmations, that the user can't spend yet

## Code

### Android

```java
conio.walletService.walletdetails(result->{
    result.analysis(details-> {
        // WalletDetails
    }, error-> {
        // Exception
    });
});
```

### iOS

```swift
conio.walletService.walletDetails { result in
    result.analysis(ifSuccess: { details in
        // WalletDetails
    }, ifFailure: { error in
        // ServiceError
    })
}
```
# Send Bitcoin
With this SDK you can send bitcoins to any other Bitcoin wallet. 
There is also a second factor to protect the operation.

## Get sendable Max Amount
First of all you will need to fetch the maximum amount the user can send, which is equal to the amount in their wallet minus the mining fees.
Conio will give you exactly the maximum amount in Satoshis that the user can send if you make a `WithdrawalFees` request if you simply pass the **destAddress** 

## Get mining fees
If the user inputs an amount lower or equal to the Max Amount you can then request the available mining-fees speeds.
Conio has an algorithm that you can use. 

### Parameters

A `WithdrawalFeesParams` struct:

- **destAddress**: the address that will receive the bitcoins
- **amount**: the bitcoin amount, in Satoshi. If you input `0` you will get the fees as if you were sending the maximum amount in the wallet
- **speed**: a specific speed (1 faster, 5 slower), if you don't specify a speed (priority) you will get an array with all the available speeds.

### Which params should you use?
- To get the `Max amount`: you just have to pass the **destAddress**
- To get the `Available Fees`: You have to use **destAddress** and **amount**. The resulting array cointains all the available speeds.

### Return

An `AvailableWithdrawalFees` struct containing:

- **absoluteFees**: total amount of the mining fees expressed in satoshi
- **amount**: the amount, expressed in satoshi, that the user can send at the requested speed
- **feePerByte**: transaction size (bytes)/ absoluteFees = feePerByte
- **transactionSpeed**: transaction priority 
- **availableFees**: an array contaning all the possible speeds

### Errors

* NOT_ENOUGH_BTC_AMOUNT
* DUST_TRANSACTION the amount you are trying to send is too small
* NO_SUCH_WITHDRAWAL_FEES_INFO: Can't calculate the mining fees 

### iOS example

```swift
// maximum amount you can send (speed 5)
let params = WithdrawalFeesParams(destAddress: "mkHS9ne12qx9pS9VojpwU5xtRd4T7X7ZUt")

// all the available speeds for a set amount: 10000 satoshi
let params = WithdrawalFeesParams(destAddress: "mkHS9ne12qx9pS9VojpwU5xtRd4T7X7ZUt", amount: 10_000)

// send everything with the fastest speed (speed 1)
let params = WithdrawalFeesParams(destAddress: "mkHS9ne12qx9pS9VojpwU5xtRd4T7X7ZUt", amount: 0, speed: .transactionSpeedType1)

conio.walletService.withdrawalFees { result in
    result.analysis(ifSuccess: { availableFees in
        // availableFees
    }, ifFailure: { error in
        // ServiceError
    })
}
```
### Android example

```java
// maximum amount you can send (speed 5)
let params = WithdrawalFeesParams(destAddress: "mkHS9ne12qx9pS9VojpwU5xtRd4T7X7ZUt")

// all the available speeds for a set amount: 10000 satoshi
let params = WithdrawalFeesParams(destAddress: "mkHS9ne12qx9pS9VojpwU5xtRd4T7X7ZUt", amount: 10_000)

// send everything with the fastest speed (speed 1)
WithdrawalFeesParams params = new WithdrawalFeesParams("mkHS9ne12qx9pS9VojpwU5xtRd4T7X7ZUt", 0L, TransactionSpeedType.SPEED_ONE);

conio.walletService.withdrawalFees(params, response -> {
    response.analysis(availableFees -> {
        // availableFees
    }, error -> {
        // ServiceError
    });
});
```

## Finalize Send - second factor

Now that you have the feePerByte you can finally send the bitcoins using the following method.
After the first attempt you will receive an error asking for a 2fa code. The user will receive an email with the code that can be used for **5 minutes**. 
You will pass this code to the SDK in the parameters of the same method.

## Parameters for the first attempt
Use a  `TransactionParams` struct:

- **address**: Bitcoin address
- **amount**: satoshi amount of the transaction
- **fee**: mining fee [Satoshi per byte](#Get-mining-fees) 

### iOS

```swift
let params = TransactionParams(
    address: "mkHS9ne12qx9pS9VojpwU5xtRd4T7X7ZUt", 
    amount: UInt64(1000), 
    feePerByte: UInt64(10)
)
conio.walletService.sendTransaction(params) { result in
    result.analysis(ifSuccess: { sentTransaction in
        // ...
    }, ifFailure: { error in
        // Get the mfa token
        if case let .mfaRequired(token: token) = error {
            let mfaToken = token
        }
    })
}
```

### Android

```java
// Chiamata senza Codice MFA ed MFA Token
TransactionParams params = new TransactionParams(
    "mkHS9ne12qx9pS9VojpwU5xtRd4T7X7ZUt",
    1000L,
    10L
);

conio.walletService.sendTransaction(params, result -> {
    result.analysis(sentTransaction -> {
        // ...
    }, error -> {
        // Get the mfa token
        if (error instanceof MfaRequiredException) {
            MfaRequiredException mfaRequiredException = (MfaRequiredException) error;
            String mfaToken = mfaRequiredException.getMfaToken();
        }
    }
    });
});
```

## Optional deep link

The user can click on a deep link found in their email like this one:

```
conio-internal://request_btc_withdrawal?code=<MFACode>
```

To avoid losing data when the user puts the app in background and then clicks on the deep link, you can save the info about the send (amount, address and fees) in the memory of the device.

## Parameters for the second attempt

To send Bitcoin you can use a `TransactionParams` struct:

- **address**: Bitcoin address
- **amount**: satoshi amount of the transaction
- **fee**: mining fee [Satoshi per byte](#Get-mining-fees) 
- **mfaCode**: the code that the user received in their email after the first attempt

## Returns

A `SentTransaction` containing:

- **transactionId**: transaction identifier
- **fee**: payed mining fees 

## Errors
- **[iOS] ServiceError.mfaRequired**: No mfaCode used or the code is incorrect. The user will receive a new code.
- **[Android] ConioError.MFA_REQUIRED**: No mfaCode used or the code is incorrect. The user will receive a new code.

* NOT_ENOUGH_BTC_AMOUNT
* DUST_TRANSACTION the amount you are trying to send is too small
* INVALID_MESSAGE_SIGNATURE 

### iOS example

```swift
let params = TransactionParams(
    address: "mkHS9ne12qx9pS9VojpwU5xtRd4T7X7ZUt", 
    amount: UInt64(1000), 
    feePerByte: UInt64(10),
    mfaToken: "OciqYgdjxJV413iHkFqgUYGk",
    mfaCode: "806157"
)

conio.walletService.sendTransaction(params) { result in
    result.analysis(ifSuccess: { sentTransaction in
        // SentTransaction
    }, ifFailure: { error in
        // ServiceError
    })
}
```

### Android example

```java
// MFA e MFA Token
TransactionParams params = new TransactionParams(
    "mkHS9ne12qx9pS9VojpwU5xtRd4T7X7ZUt", 
    1000L,
    10L,
    "OciqYgdjxJV413iHkFqgUYGk",
    "806157"
);

conio.walletService.sendTransaction(params, result -> {
    result.analysis(sentTransaction -> {
        // SentTransaction
    }, error -> {
        // Exception
    });
});
```

# Wallet backup code 
Show the wallet backup code: a list of 12 words. 

## Returns

A `MnemonicWords` containing an array with 12 strings in it.

## Errors
- **missingMnemonic**: failed to retrieve the backup code

### Android

```java
conio.walletService.readMnemonic(result->{
    result.analysis(mnemonicWords-> {
        // MnemonicWords
    }, error-> {
        // Exception
    });
});
```

### iOS

```swift
conio.walletService.readMnemonic { result in 
    result.analysis(ifSuccess: { mnemonicWords in
        // MnemonicWords
    }, ifFailure: { error in
        // ServiceError
    })
}
```
