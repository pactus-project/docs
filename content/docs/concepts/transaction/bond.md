---
title: Bond Transaction
weight: 4
math: false
---

Bond transaction is used to bond stake to a [validator](/docs/blockchain/validator/).
If the validator does not exist, it will be created.
Once a bond transaction committed, the validator cannot participate in the
[sortition algorithm](/docs/consensus/sortition/) for 1 hour.
This is called the "bond interval" and is defined in the
[consensus parameter](/docs/consensus/parameters/).

## Payload Structure

The bond transaction has a payload consists the following fields:

| Size                | Field            |
| ------------------- | ---------------- |
| 21 bytes            | Sender address   |
| 21 bytes            | Receiver address |
| 96 bytes (optional) | Public key       |
| Variant             | Amount           |

- **Sender address** is the address of the sender [account](/docs/blockchain/account/).
- **Receiver address** is the address of the receiver validator.
- **Public key** is the validator's public key. If the validator does not exist yet,
  the public key should be set, otherwise it should left empty.
- **Amount** is the amount of coins that should be staked or bonded.
