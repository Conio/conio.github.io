# Installation

## Requires
* iOS 10+
* Autoconf 
* Automake

## Cocoapods install

Add this line to your podfile:

```ruby
# The ConioSDK Core
pod 'ConioSDK', :git => 'git@bitbucket.org:squadrone/conio-swift-sdk.git', :branch => 'master'

# BitcoinKit for encryption purposes
pod 'BitcoinKit', :git => 'https://github.com/Conio/BitcoinKit.git', :branch => 'keyconvert'
```

Then use the command: `pod install` 

---
---
## Troubleshooting
If you get the following error:
```bash
autoreconf: failed to run aclocal: No such file or directory
```
Try the following command:

 `brew install autoconf && brew install automake`. 

---

If you get the following error:
```
Can't exec "/opt/local/bin/aclocal": No such file or directory
```
Uninstall MacPorts with:

`sudo port -fp uninstall --follow-dependents installed`
