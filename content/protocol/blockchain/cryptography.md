---
title: Cryptography
weight: 7
---

The Pactus blockchain uses various cryptographic algorithms, including hashing and digital signature schemes,
to protect user data and secure transactions.

## Hashing Algorithm

Pactus uses the [Blake2b](https://www.blake2.net/) hashing algorithm.
Blake2b is a fast and secure cryptographic hash function that produces unique digital fingerprints of data.

## Signature Schemes

Pactus supports several signature schemes for different purposes.

### BLS Signatures

[BLS](https://datatracker.ietf.org/doc/draft-irtf-cfrg-bls-signature/) (Boneh–Lynn–Shacham) is the primary signature scheme
used by validators and BLS-based accounts.
BLS public keys are 96 bytes and use the G2 subgroup of the BLS12-381 curve.
BLS is a threshold signature scheme with two notable properties:

#### Signature Aggregation

BLS signatures can be aggregated — multiple individual signatures can be combined into a single signature
without increasing the overall size. This is useful for consensus where many validators sign the same message.

#### Non-Malleability

BLS signatures are non-malleable: it is impossible to produce two different valid signatures for the same message.
Each message has exactly one valid signature.

### Ed25519 Signatures

[Ed25519](https://www.rfc-editor.org/rfc/rfc8032.txt) is supported for account addresses
(see [PIP-52](https://pips.pactus.org/PIPs/pip-52)).
Ed25519 provides strong security with compact 32-byte public keys and fast performance.
Ed25519 account addresses start with `pc1r...`.

### secp256k1 Signatures

[secp256k1](https://www.secg.org/sec2-v2.pdf) (ECDSA) is supported for account addresses
(see [PIP-53](https://pips.pactus.org/PIPs/pip-53)).
This is the same curve used by Bitcoin, with 33-byte compressed public keys, enabling compatibility with existing wallet tools.
secp256k1 account addresses start with `pc1y...`.

## Address Types

Addresses in Pactus include a type that indicates their intended usage
(see [PIP-8](https://pips.pactus.org/PIPs/pip-8)):

| **Type** | **Usage**         | **Address Prefix** | **Derivation Path**             |
| -------- | ----------------- | ------------------ | ------------------------------- |
| 1        | Validator         | `pc1p...`          | `m/12381'/21888'/1'/index`      |
| 2        | BLS Account       | `pc1z...`          | `m/12381'/21888'/2'/index`      |
| 3        | Ed25519 Account   | `pc1r...`          | `m/44'/21888'/3'/index'`        |
| 4        | secp256k1 Account | `pc1y...`          | `m/44'/21888'/4'/index'`        |

## HD Key Derivation

Pactus supports Hierarchical Deterministic (HD) key derivation for wallets.
This allows a single master seed to generate a tree of keys in a predictable way.

BLS HD derivation follows [PIP-11](https://pips.pactus.org/PIPs/pip-11),
which defines a standard for BLS12-381 HD key chains based on
[BIP-0032](https://github.com/bitcoin/bips/blob/master/bip-0032.mediawiki).
Ed25519 and secp256k1 HD derivation follow
[SLIP-10](https://github.com/satoshilabs/slips/blob/master/slip-0010.md).
