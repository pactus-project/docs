---
title: Address
weight: 8
---

# Address

An address is a unique identifier that is used to send and receive transactions on the Pactus blockchain.
It is represented as a string of 42 alphanumeric characters and always begins with the letters "pc1".
Here is an example of an address on the Pactus blockchain:

```text
pc1p4e92hx0erqyx939crndvthvpn7qcdhefc9r6s7
```

## Address Structure

An address in the Pactus blockchain is made up of 21 bytes and it is derived from the public key.
The first byte of the address specifies the address type,
while the remaining 20 bytes represent the hash of the public key.
The hash function used is [RIPEMD-160](https://en.wikipedia.org/wiki/RIPEMD#RIPEMD-160_hashes),
which is applied after [Blake2b](/protocol/blockchain/cryptography/#hashing-algorithm)):
The resulting byte array is then converted into a bech32m[^first] string.

![Pactus address structure](/images/pactus-address.png)

## Address Type

The address type specifies the type of the address and its defined as below
(see [PIP-8](https://pips.pactus.org/PIPs/pip-8)):

- 0: Treasury address
- 1: Validator address
- 2: BLS Account address
- 3: Ed25519 Account address
- 4: secp256k1 Account address

## Address Derivation

An address is derived from the compressed public key as follows:

```text
hash_256 = Blake2b_256(compressed_public_key)     // 32 bytes
hash_160 = RIPEMD160(hash_256)                    // 20 bytes
raw_addr = [address_type] + hash_160              // 21 bytes
address  = Bech32m("pc", address_type, hash_160)
```

The address type is chosen based on how the address will be used:

| **Public Key**                 | **Address Type** | **Prefix** |
| ------------------------------ | ---------------- | ---------- |
| BLS (G2, 96 bytes) → validator | `1`              | `pc1p...`  |
| BLS (G2, 96 bytes) → account   | `2`              | `pc1z...`  |
| Ed25519 (32 bytes)             | `3`              | `pc1r...`  |
| secp256k1 (33 bytes)           | `4`              | `pc1y...`  |

## Treasury Address

The Treasury address on the Pactus blockchain is a fixed address that is defined as follows:

```text
TreasuryAddress: 000000000000000000000000000000000000000000
```

The address type for the Treasury address is set to zero, which
means there is no key associated with the Treasury address.
The remaining characters of the address are all zeros.

[^first]: [bech32m address format](https://github.com/bitcoin/bips/blob/master/bip-0350.mediawiki)
