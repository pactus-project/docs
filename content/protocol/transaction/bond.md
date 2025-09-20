---
title: Bond Transaction
weight: 3
math: false
---

Bond transaction is used to bond stake to a [validator](/protocol/blockchain/validator/).
If the validator does not exist, it will be created.
Once a bond transaction committed, the validator cannot participate in the
[sortition algorithm](/protocol/consensus/sortition/) for 1 hour.
This is called the "bond interval" and is defined in the
[consensus parameter](/protocol/consensus/parameters/).
Validators within the committee cannot increase their stake.
Therefore, bond transactions will be processed only when the validators are not in the committee.

The [Payload Type](/protocol/transaction/format/#payload-type) for Bond is 2.

## Payload Structure

The bond transaction has a payload consists the following fields:

| Field                 | Size     |
| --------------------- | -------- |
| Sender address        | 21 bytes |
| Receiver address      | 21 bytes |
| Public key (optional) | 96 bytes |
| Amount                | Variant  |

- **Sender address** is the address of the sender [account](/protocol/blockchain/account/).
- **Receiver address** is the address of the receiver validator.
- **Public key** is the validator's public key. If the validator does not exist yet,
  the public key should be set, otherwise it should left empty.
- **Amount** is the amount of coins that should be staked or bonded.
