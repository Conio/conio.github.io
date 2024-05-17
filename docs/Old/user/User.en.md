# User operations

## Terms and conditions

Using this operation you can retrieve the `Acceptances` (terms and conditions), T&C URL and Privacy Policy URL that the user has to accept during the signup.

### Parameters

An object `LegalAcceptancesParams` with the language you want.

### Returns

A `LegalAcceptances` object containing `Acceptances`, the URL `Terms of service`, the URL `Privacy Policies` and the pre-contractual info URL.

### Acceptances localization

An `Acceptance` has 2 localization keys: one for the title and one for the content.

### Code

#### Android

```java
LegalAcceptancesParams params =
    new LegalAcceptancesParams(Language.ITALIAN);
conio.userService.getLegalAcceptances(params, result -> {
    result.analysis(acceptances -> {
        // LegalAcceptances
    }, error -> {
        // Exception
    });
});
```

#### iOS

```swift
let params = LegalAcceptancesParams(language: .italian)

conio.userService.getLegalAcceptances(params: params) { result in
    result.analysis(ifSuccess: { legalAcceptances in
        // LegalAcceptances
    }, ifFailure: { error in
        // ServiceError
    })
}
```

## Signup

To use the wallet the user has to be authenticated. If it's the first time you can authenticate using the signup method, otherwise you have to use the login method.

### Parameters

An `Account` struct containing:

- ***login***: `Login` on iOS or `UserLogin` on Android: username and password of the user.
- ***acceptances***: `Acceptances` containing booleans about the user consent to T&C
- ***cryptoRequest***: create a `CryptoRequest`: [Crypto Request Creation](#Crypto-Request-Creation)

### Crypto Request Creation

To generate a `Crypto Request`, you have to sign the string: `dataString` (create one by following the example below), using the function sha256 and the private key. The following lines of code are just an example. The actual implementation of the signing algorithm to include in the `CryptoRequest` is up to the client.

#### Java Example

```java
    String proofId = UUID.randomUUID().toString();
    long proofExpiration =
        new Date()
        .tenMinutesFromNow()
        .millis();

    String userLevel = "A smart level"; // Es. "Advanced" to get adavanced limits
    String userId = login.username;
    String iban = "IBAN"; // It should be a real iban
    String email = "user@email.com";
    String firstName = "Mario";
    String lastName = "Rossi";

    String[] data = {
        proofId,
        "SIGNUP",
        userId,
        userLevel,
        String.valueOf(proofExpiration),
        iban,
        email,
        firstName,
        lastName
    };

    String dataString = join("|", data);

    PrivateKey privateKey = new PrivateKey("key.pem");
    RsaSigner rsa = new RsaSigner(privateKey);

    String signature =
        rsa
        .sign("sha256", dataString)
        .toLowercase();

    byte[] cryptoProof = fromHexToBytes(signature);
```

#### Swift Example

```swift
    let proofID = UUID().uuidString
    let proofExpiration: UInt64 = UInt64(Date())
    let userLevel = "A smart level" // Es. "Advanced" to get adavanced limits
    let userID = login.username
    let iban = "IBAN" // It should be a real iban
    let email = "user@email.com"
    let firstName = "Mario"
    let lastName = "Rossi"

    let data = [
        proofID,
        "SIGNUP",
        userID,
        userLevel,
        String(proofExpiration),
        iban,
        firstName,
        lastName
    ]

    let dataString = data.joined(separator: "|")

    let cryptoProof = Crypto.sign(
        privateKey: privateKey,
        digestType: .sha256
    )

    let cryptoRequest = CryptoRequest(
        proofID: proofID,
        cryptoProof: cryptoProof.data,
        proofExpiration: proofExpiration,
        userID: userID,
        userLevel: userLevel,
        iban: iban,
        email: email,
        firstName: firstName,
        lastName: lastName
    )
```

### Returns

An object `Acceptances` confirming which T&C the user approved during the signup.

### Errori
* `INVALID_IBAN`
* `CRYPTO_PROOF_EXPIRED`
* `INVALID_CRYPTO_PROOF` Crypto proof was signed incorrectly
* `CARDS_SERVICE_COULD_NOT_CREATE_PAYER` Internal error of the payment system
* `DUPLICATE_EMAIL_ADDRESS`
* `WALLET_ALREADY_OWNED_BY_ANOTHER_USER`
* `CLIENT_SUPPORT_ACCEPTANCE_NOT_ACCEPTED` Required acceptance
* `APP_IMPROVEMENT_ACCEPTANCE_NOT_ACCEPTED` Required acceptance


### Code

#### Android

```java
UserLogin login = new UserLogin("lemonade", "secretword");

// Build the acceptances list with the user choices result
Acceptance appImprovement
    = new Acceptance(AcceptanceType.APP_IMPROVEMENT, true);
Acceptance clientSupport
    = new Acceptance(AcceptanceType.CLIENT_SUPPORT, true);

ArrayList<Acceptance> acceptanceList = new ArrayList<>();
acceptanceList.add(appImprovement);
acceptanceList.add(clientSupport);

Acceptances acceptances = new Acceptances(acceptanceList);

// Your crypto request implementation
CryptoRequest cryptoRequest = buildCryptoRequest();

Account account = new Account(login, acceptances, cryptoRequest);
conio.userService.signup(account, result -> {
    result.analysis(acceptances -> {
        // Acceptances
    }, error -> {
        // Exception
    });
});
```

#### iOS

```swift

let login = Login(username: "lemonade", password: "secretword")

// Your crypto request implementation
let cryptoRequest = buildCryptoRequest()

// Build the acceptances list with the user choices result
let appImprovement =
    Acceptance(type: .appImprovement, isAccepted: true)
let clientSupport =
    Acceptance(type: .clientSupport, isAccepted: true)

let acceptancesList = [appImprovement, clientSupport]
let acceptances = Acceptances(acceptances: acceptancesList)

let account = Account(
    login: login,
    acceptances: acceptances,
    cryptoRequest: cryptoRequest
)

conio.userService.signup(with: account) { result in
    result.analysis(ifSuccess: { acceptances in
        // Acceptances
    }, ifFailure: { error in
        // ServiceError
    })
}
```

## Login

Using the login operation you can authenticate to Conio. It is **recommended** to perform this operation every time the app is started.

### Parameters

An object, called `Login` on iOS or `UserLogin` on Android, containing:

- **username**
- **password**

### Returns

An `Acceptances` object with the T&C that the user accepted on signup.
### Code

#### Android

```java
UserLogin login = new UserLogin("lemonade", "secretword");
conio.userService.login(login, result -> {
    result.analysis(acceptances -> {
        // Acceptances
    }, error -> {
        // Exception
    });
});
```

#### iOS

```swift
let login = Login(username: "lemonade",password: "secretword")
conio.userService.login(with: login) { result in
    result.analysis(ifSuccess: { acceptances in
        // Acceptances
    }, ifFailure: { error in
        // ServiceError
    })
}
```

## Logout

Disconnect from Conio.

### Returns

A `boolean` with the result of the operation.

### Code

#### Android

```java
conio.userService.logout(result -> {
    result.analysis(success -> {
        // Boolean
    }, error -> {
        // Exception
    });
});
```

#### iOS

```swift
conio.userService.logout { result in
    result.analysis(ifSuccess: { success in
        // Boolean
    }, ifFailure: { error in
        // ServiceError
    })
}
```

## Change Email

Using this operation you can update Conio user email.

### Method

`userService.changeEmail`

### Parameters

A `ChangeEmailParams` object type.

- ***newEmail***: `String` type, it is the new value used to update actual user email.

### Returns
#### Android
A `Success` object type if the operation finish with success.

#### iOS
A `Void` object type if the operation finish with success.


### Code

#### Android

```java
ChangeEmailParams params = new ChangeEmailParams("newEmail@conio.com");

conio.userService.changeEmail(params).asCallback(result -> result.analysis(
        activityList -> { /* Success */ },
        error -> { /* ... */ }
));
```

#### iOS

```swift
let params = ChangeEmailParams(newEmail: "newEmail@conio.com")
conio.userService.changeEmail(with: params).asCallback { result in
    switch result {
    case .failure(let error):
        /* ... */
    case .success:
        /* Success */
    }
}
```
