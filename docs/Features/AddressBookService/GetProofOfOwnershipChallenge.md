# Get Proof Of Ownership Challenge

## Overview

`getProofOfOwnershipChallenge` API requests a proof-of-ownership challenge for a given wallet address. This method initiates the verification process by generating a challenge message that the wallet owner must sign in order to prove control over the specified address.

## Params

The `ProofOfOwnershipChallengeParams` containing the wallet address for which the challenge should be generated.

- wallet address: the wallet address for which the proof-of-ownership challenge should be generated.

## Result

The `ProofOfOwnershipChallengeResult` contains the challenge message that must be signed to prove ownership of the wallet address.

- message: the challenge message that the wallet owner must sign (accordingly with the [BIP 137 standard](https://bips.dev/137/)).

## Code

### iOS
```swift
let params = ProofOfOwnershipChallengeParams.make(walletAddress: ...)

addressBookService
    .getProofOfOwnershipChallenge(params: params)
    .asPublisher()
    .sink { result in
        // ...
    }
```