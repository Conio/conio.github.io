# Common errors

List of common errors that can be returned by any service:

- `OnNetwork`: there is no internet connection or the *base url* provided as configuration is wrong.
- `OutdatedSdk`: this Conio SDK version can no longer be used, you need to update it to a newer version.
- `Unauthorized`: the service launched requires authentication, but there is no valid session.
- `UnderMaintenance`: the Conio services are under maintenance.
- `Unknown`: an unexpected error.