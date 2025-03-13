# iOS Installation

## Prerequisites

- iOS 13+
- Swift 5.9

## Swift Package Manger

### Via Xcode

1. In Xcode, install Conio B2B SDK by navigating to *File > Add Packages*
2. In the prompt that appears, insert the repository:

```
git@bitbucket.org:squadrone/conio-sdk-b2b-ios.git
```
or 
```
https://bitbucket.org/squadrone/conio-sdk-b2b-ios.git
```

### Via `Package.swift`

Simply add the following lines to `dependencies` of your `Package.swift` manifest:
```
dependencies: [
  .package(url: "git@bitbucket.org:squadrone/conio-sdk-b2b-ios.git")
  // ...
],
```

Note: in order to correctly fetch package you will need to have access to project repository.

## Troubleshooting

If you get the following error:

`autoreconf: failed to run aclocal: No such file or directory` 

try the following command using [Brew](https://brew.sh/index_it):

`brew install autoconf && brew install automake`

If you get the following error:
`Can't exec "/opt/local/bin/aclocal": No such file or directory`
Uninstall MacPorts with:
`sudo port -fp uninstall --follow-dependents installed`