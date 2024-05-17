# Crypto Request

Alcune funzionalità del SDK Conio sono protette da un meccanismo chiamato **Crypto Request**, che aggiunge un livello di sicurezza ulteriore all'invio di alcuni parametri, tramite una firma crittografica.

Le richieste che sfruttano questo meccanismo sono riconoscibili dalla presenza della proprietà `cryptoRequest`, di tipo `[Name]CryptoRequest`, presente nella funzione di costruzione (costruttore o metodo factory) del oggetto da passare come parametro all'operazione. In particolare, le funzionalità protette da questo meccanismo sono:

1. `userService.signup`, registrazione dell'utente (`SignupCryptoRequest`);
2. `userService.login`, autenticazione dell'utente (`LoginCryptoRequest`);
4. `exchangeService.purchase`, acquisto di Bitcoin (`BidCryptoRequest`);
3. `exchangeService.sell`, vendita di Bitcoin (`AskCryptoRequest`).

La costruzione di ogni proprietà di tipo `[Name]CryptoRequest` necessita di un parametro `cryptoProof`, un **array di byte**, ottenuto tramite firma `RSA` del hash `SHA256` della concatenazione (con separatore "|") ordinata delle altre proprietà del tipo `[Name]CryptoRequest` (come descritto per ogni tipo `[Name]CryptoRequest` nel apposito paragrafo).

```
NFC=<implementazione algoritmo di conversione stringa - array di byte>
SHA256=<implementazione algoritmo di hashing SHA256>
RSA_SIGN=<implementazione algoritmo di firma RSA>

CRYPTO_PROOF = RSA_SIGN(SHA256(NFC(DATA_TO_SIGN)))
```

## Creazione SignupCryptoRequest

### Proprietà

- **proofID**: di tipo `String`, identificativo della Crypto Request;
- **userID**: di tipo `String`, identificativo esterno del utente;
- **userLevel**: di tipo `String`, livello del utente che ne stabilisce i limiti di compravendita;
- **proofExpiration**: di tipo `long`, istante temporale dopo il quale la Crypto Request non è più considerata valida;
- **@Opzionale iban**: di tipo `String`, iban del conto bancario associato all'utente, utilizzato come metodo di pagamento per le operazioni di vendita;
- **email**: di tipo `String`, email dell'utente;
- **firstName**: di tipo `String`, nome dell'utente;
- **lastName**: di tipo `String`, cognome dell'utente;

### DATA_TO_SIGN

```
DATA_TO_SIGN="<proofID>|SIGNUP|<userID>|<userLevel>|<proofExpiration>|<email>|<firstName>|<lastName>"

or

DATA_TO_SIGN="<proofID>|SIGNUP|<userID>|<userLevel>|<proofExpiration>|<iban>|<email>|<firstName>|<lastName>"
```

**Nota**: il campo **iban** è opzionale, pertanto, se non lo si inserisce nella `SignupCryptoReqeust`, va rimosso anche dalla stringa `DATA_TO_SIGN` (insieme al separatore "|")

## Creazione LoginCryptoRequest

### Proprietà

- **userID**: di tipo `String`, identificativo esterno del utente;
- **proofExpiration**: di tipo `long`, istante temporale dopo il quale la Crypto Request non è più considerata valida;

### DATA_TO_SIGN

```
DATA_TO_SIGN="<userID>|LOGIN|<proofExpiration>"
```

## Creazione AskCryptoRequest

### Proprietà

- **proofID**: di tipo `String`, identificativo della Crypto Request;
- **askID**: di tipo `String`, identificativo della `CreatedAsk` che si vuole finalizzare;
- **userID**: di tipo `String`, identificativo esterno del utente;
- **proofExpiration**: di tipo `long`, istante temporale dopo il quale la Crypto Request non è più considerata valida;

### DATA_TO_SIGN

```
DATA_TO_SIGN="<proofID>|PAY_FOR_ASK|<askID>|<userID>|<proofExpiration>"
```

## Creazione BidCryptoRequest

### Proprietà

- **proofID**: di tipo `String`, identificativo della Crypto Request;
- **bidID**: di tipo `String`, identificativo dell `CreatedBid` che si vuole finalizzare;
- **userID**: di tipo `String`, identificativo esterno del utente;
- **proofExpiration**: di tipo `long`, istante temporale dopo il quale la Crypto Request non è più considerata valida;

### DATA_TO_SIGN

```
DATA_TO_SIGN="<proofID>|PAY_FOR_BID_WT|<bidID>|<userID>|<proofExpiration>"
```
