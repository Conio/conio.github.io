# Operazioni sull'utente

## [Recupero dei termini di servizio](recupero-dei-termini-di-servizio)

L'oggetto `LegalAcceptancesResult` restituito contiene una lista di `Acceptance`, ciascuna delle quali rappresenta una specifica condizione da presentare all'utente. Per ogni acceptance sono disponibili un identificativo (id), un titolo (title), un testo descrittivo (body), un eventuale URL del documento (url), l'indicazione se l'accettazione è obbligatoria (isMandatory) e una lista di tag (tags) che ne identificano la tipologia, ad esempio i Termini e Condizioni o le condizioni relative al marketing.

Il testo descrittivo e l'URL del documento possono essere assenti. I tag consentono di riconoscere la natura delle singole condizioni senza fare affidamento su un tipo di acceptance predefinito.

### Metodo

`userService.getLegalAcceptances`

### Parametri

Un oggetto di tipo `LegalAcceptancesParams` contenente la lingua di riferimento per ottenere le acceptances e gli url delle pagine web da mostrare all'utente.

### Risposta

Un oggetto di tipo `LegalAcceptancesResult`, contenente la lista delle `Acceptance` da presentare all'utente. Ogni elemento include l'identificativo, il titolo, il testo descrittivo opzionale, l'eventuale URL del documento, l'indicazione di obbligatorietà e i tag associati.

### Codice

#### Android

```java
LegalAcceptancesParams params = new LegalAcceptancesParams(Language.ITALIAN);

conio.userService.getLegalAcceptances(params)
    .asCallback(result -> result.analysis(
        acceptances -> { /* Handle LegalAcceptances */ },
        error -> { /* Handle error */ }
    ));
```

#### iOS

```swift
let params = LegalAcceptancesParams(language: .italian)

conio.userService.getLegalAcceptances(params: params).asCallback { result in
    switch result {
    case .success(let acceptances):
        // LegalAcceptances
    case .failure(let error):
        // Operation Error
    }
}
```

## Recupero dello stato dei termini e condizioni

Questa operazione consente di recuperare lo stato delle accettazioni dei Termini e Condizioni dell'utente. Il risultato contiene una lista di `Acceptance`, ciascuna identificata da un ID e caratterizzata da uno stato che indica se la condizione deve ancora essere accettata, è stata accettata oppure è stata rifiutata. Per le accettazioni già effettuate, può essere disponibile anche la data di accettazione (`acceptedAt`).

### Metodo

`userService.getUserTc`

### Risposta

Un oggetto di tipo `UserTcResult`, contenente la lista delle `Acceptance` relative all'utente. Ogni elemento include:
- `id`: identificativo dell'accettazione.
- `status`: stato dell'accettazione, rappresentato da uno dei seguenti valori:
    - `toAccept`: la condizione deve ancora essere accettata.
    - `accepted`: la condizione è stata accettata.
    - `rejected`: la condizione è stata rifiutata.
    - `acceptedAt`: timestamp dell'accettazione se disponibile, altrimenti nil.

### Codice

#### Android

```java
conio.userService.getUserTc()
    .asCallback(result -> result.analysis(
        userTc -> { /* Handle UserTc */ },
        error -> { /* Handle error */ }
    ));
```

#### iOS

```swift
conio.userService.getUserTc().asCallback { result in
    switch result {
    case .success(let userTc):
        // UserTc
    case .failure(let error):
        // Operation Error
    }
}
```

## Accettazione delle nuove condizioni legali

Questa operazione consente di inviare l'accettazione delle nuove condizioni legali e dei Termini e Condizioni da parte dell'utente. Le accettazioni da inviare vengono specificate tramite il parametro `AcceptNewLegalAcceptancesParams`, che contiene l'oggetto `Acceptances` con le scelte effettuate dall'utente. È inoltre possibile fornire le credenziali Conio tramite il parametro opzionale `credentials`.

### Metodo

`userService.acceptNewLegalAcceptances`

### Parametri

Un oggetto di tipo `AcceptNewLegalAcceptancesParams`, contenente:
- `acceptances`: un oggetto di tipo `Acceptances` che descrive le accettazioni da inviare.
- `credentials`: un oggetto opzionale di tipo `ConioCredentials`, utilizzato per fornire le credenziali Conio. Se non specificato, il valore predefinito è nil.

### Risposta

Un `ServiceConsumer<Void>` che consente di verificare l'esito dell'operazione. In caso di successo, l'operazione non restituisce alcun dato.

### Codice

#### Android

```java
AcceptNewLegalAcceptancesParams params = new AcceptNewLegalAcceptancesParams(acceptances, credentials);

conio.userService.acceptNewLegalAcceptances(params)
    .asCallback(result -> result.analysis(
        success -> { /* Handle success */ },
        error -> { /* Handle error */ }
    ));
```

#### iOS

```swift
let params = AcceptNewLegalAcceptancesParams(acceptances: ..., credentials: ...)

conio.userService.acceptNewLegalAcceptances().asCallback { result in
    switch result {
    case .success:
        // Success
    case .failure(let error):
        // Operation Error
    }
}
```

## Autenticazione

Per poter operare con il portafoglio Conio occorre essere autenticati. Se è la prima volta che l'utente usa il servizio ci si può autenticare con il metodo `userService.signup`, altrimenti con il metodo `userService.login`.

## Signup

L'operazione di signup permette di creare un nuovo utente Conio.

### Metodo

`userService.signup`

### Parametri

Un oggetto di tipo `SignupParams`, costruito tramite il metodo `SignupParams.createCryptoSignup` con:

- ***acceptances***: di tipo `Acceptances` con l'esito della conferma ai termini di servizio da parte dell'utente, recuperati tramite le [`LegalAcceptances`](recupero-dei-termini-di-servizio);

- ***credentials***: di tipo `ConioCredentials` con username e password dell'utente;

- ***cryptoRequest***: di tipo `SignupCryptoRequest`, che specifica ulteriori parametri comprovati da una firma, come descritto in [creazione della SignupCryptoRequest](../operation/CryptoRequest.md#Creazione-SignupCryptoRequest).

### Risposta

Un oggetto di tipo `Success` che indica che l'utente è stato autenticato.

### Errori

- [ConioError](../operation/Operation.md#ConioError):

    * `APP_IMPROVEMENT_ACCEPTANCE_NOT_ACCEPTED` Acceptance obbligatoria;
    * `CLIENT_SUPPORT_ACCEPTANCE_NOT_ACCEPTED` Acceptance obbligatoria;
    * `CRYPTO_PROOF_EXPIRED` La crypto proof è scaduta;
    * `INVALID_CRYPTO_PROOF` La crypto proof non è correttamente firmata;
    * `DUPLICATE_EMAIL_ADDRESS` Indirizzo email duplicato;
    * `INVALID_IBAN` IBAN non valido;
    * `WALLET_ALREADY_OWNED_BY_ANOTHER_USER` Il wallet è già utilizzato da un altro utente;
    * `CARDS_SERVICE_COULD_NOT_CREATE_PAYER` Errore interno del sottosistema di pagamento.


### Codice

#### Android

```java
// vedi "Creazione SignupCryptoRequest"
SignupCryptoRequest cryptoRequest = new SignupCryptoRequest(...);
ConioCredentials credentials = new ConioCredentials("username", "password");
Acceptances acceptances = new Acceptances(Arrays.asList(
    new Acceptance(AcceptanceType.CLIENT_SUPPORT, true),
    new Acceptance(AcceptanceType.APP_IMPROVEMENT, true)
));

SignupParams params = SignupParams.createCryptoSignup(acceptances, credentials, cryptoRequest);

conio.userService.signup(params)
    .asCallback(result -> result.analysis(
        success -> { /* Handle success */ },
        error -> { /* Handle error */ }
    ));
```

#### iOS

```swift
// vedi "Creazione SignupCryptoRequest"

let credentials = ConioCredentials(username: "username", password: "password")

 var acceptancesList = [Acceptance]()
        acceptancesList.append(.init(type: .appImprovement, isAccepted: true))
        acceptancesList.append(.init(type: .clientSupport, isAccepted: true))
let acceptances = Acceptances(acceptances: acceptancesList)
let cryptoRequest = SignupCryptoRequest.init(proofID: "", cryptoProof: Data(), proofExpiration: 0, externalUserID: "", userLevel: "", iban: "", email: "", firstName: "", lastName: "")
let signupParams = SignupParams.createCryptoSignup(credentials: credentials, acceptances: acceptances, cryptoRequest: cryptoRequest)

conio.userService.signup(params: params).asCallback { result in
    switch result {
    case .success:
        // Handle Succes
    case .failure(let error):
        // Operation Error
    }
}
```


## Login

L'operazione di login permette di autenticarsi a Conio. È **raccomandabile** eseguire questa operazione ad ogni avvio dell'applicazione, similmente a come avviene per altri servizi terzi.

### Metodo

`userService.login`

### Parametri

Un oggetto di tipo `LoginParams`, costruito tramite il metodo `LoginParams.createCryptoLogin` con:

- **credentials**: di tipo `ConioCredentials` con username e password dell'utente

- **cryptoRequest**: di tipo `LoginCryptoRequest`, che specifica ulteriori parametri comprovati da una firma, come descritto in [creazione della LoginCryptoRequest](../operation/CryptoRequest.md#Creazione-LoginCryptoRequest).

### Risposta

Un oggetto di tipo `Success` che indica che l'utente è stato autenticato.

### Errori

- [Non autorizzato](../operation/Operation.md#Non-autorizzato)

### Codice

#### Android

```java
LoginCryptoRequest cryptoRequest = new LoginCryptoRequest(...);
ConioCredentials credentials = new ConioCredentials("username", "password");

LoginParams params = LoginParams.createCryptoLogin(credentials, cryptoRequest);

conio.userService.login(params)
    .asCallback(result -> result.analysis(
        success -> { /* Handle success */ },
        error -> { /* Handle error */ }
    ));
```

#### iOS

```swift
let params = LoginParams(username: "lemonade", password: "secretword", loginCryptoRequest: <LoginCryptoRequest>)
conio.userService.login(params: params).asCallback { result in
    switch result {
    case .success:
        // success
    case .failure(let error):
        // Operation Error
    }
}
```


## Logout

Consente di disconnettere l'utenza Conio.

### Metodo

`userService.logout`

### Risposta

Un oggetto di tipo `Success` che indica che l'utente è stato disconnesso.

### Codice

#### Android

```java
conio.userService.logout()
    .asCallback(result -> result.analysis(
        success -> { /* Handle success */ },
        error -> { /* Handle error */ }
    ));
```

#### iOS

```swift
conio.userService.logout().asCallback { result in
    switch result {
    case .success:
        // success
    case .failure(let error):
        // Operation Error
    }
}
```

## Change Email

Consente di modificare l'email associata all'utenza Conio.

### Metodo

`userService.changeEmail`

### Parametri

Un oggetto di tipo `CryptoChangeEmailParams`.

- ***newEmail***: di tipo `String`, è il nuovo valore utilizzato per modificare l'attuale email dell'utente.

### Risposta
#### Android
Un oggetto di tipo `Success` che indica se l'email dell'utente è stata modificata correttamente.

#### iOS
Un oggetto di tipo `Void` che indica se l'email dell'utente è stata modificata correttamente.


### Codice

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
