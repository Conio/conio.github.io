# Installazione

## Prerequisiti
* SDK supporta iOS 10+
* Autoconf installato
* Automake installato

## Installazione con Cocoapods

L'SDK Conio è disponibile come Pod ed è possibile includerla nei progetti aggiungendo le seguenti righe al Podfile:

```ruby
# The ConioSDK Core
pod 'ConioSDK', :git => 'git@bitbucket.org:squadrone/conio-swift-sdk.git', :branch => 'master'

# BitcoinKit for encryption purposes
pod 'BitcoinKit', :git => 'https://github.com/Conio/BitcoinKit.git', :branch => 'keyconvert'
```

Eseguire il comando `pod install` nella cartella per ottenere l'SDK.

---
---
## Possibili Errori nell'installazione
Se si dovesse verificare il seguente messaggio di errore: 
```bash
autoreconf: failed to run aclocal: No such file or directory
```
Eseguire il comando:

 `brew install autoconf && brew install automake`. 

---

Se si dovesse verificare il seguente messaggio di errore: 
```
Can't exec "/opt/local/bin/aclocal": No such file or directory
```
Disinstallare dal sistema MacPorts eseguendo:

`sudo port -fp uninstall --follow-dependents installed`
