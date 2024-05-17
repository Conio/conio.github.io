# Installazione

## Prerequisiti
* SDK supporta iOS 10+
* [Autoconf](https://www.gnu.org/software/autoconf/) installato
* [Automake](https://www.gnu.org/software/automake/) installato
* [Libtool](https://www.gnu.org/software/libtool/) installato

È consigliato l'utilizzo del gestori di pacchetti MacOS [Brew](https://brew.sh/index_it) per l'installazione di `Autoconf`, `Automake` e `Libtool`.

```
# Install Brew
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# Install Autoconf, Automake and Libtool
brew install autoconf automake libtool
```

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
