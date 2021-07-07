# Operazioni sull'utente

## Recupero dei termini di servizio

Questa operazione consente di recuperare le `LegalAcceptances`, ovvero le condizioni che l'utente potrà/dovrà accettare in fase di signup (scelte che, durante l'[operazione signup](#signup), dovranno essere descritte tramite la classe `Acceptances`).
L'oggetto `LegalAcceptances` recuperato conterrà gli url per mostrare le pagine dei Termini di Servizio e Privacy Policies di Conio e il dettaglio delle *acceptances* (`AcceptanceDetail`) che l'utente dovrà o meno accettare.

### Metodo

`userService.getLegalAcceptances`

### Parametri

Un oggetto di tipo `LegalAcceptancesParams` contenente la lingua di riferimento per ottenere le acceptances e gli url delle pagine web da mostrare all'utente.

### Risposta

Un oggetto di tipo `LegalAcceptances` contenente la lista degli `AcceptanceDetail`, lo url dei *Termini di Servizio* e quello delle *Privacy Policies*.

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

conio.userService.signup(params: params).asCallback { result in
    switch result {
    case .success(let acceptances):
        // LegalAcceptances
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

- ***acceptances***: di tipo `Acceptances` con l'esito della conferma ai termini di servizio da parte dell'utente, [recuperati tramite le `LegalAcceptances`](#recupero-dei-termini-di-servizio);

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
