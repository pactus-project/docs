---
title: Sortition Transaction
weight: 5
math: false
---

Sortition transaction is used to enter a [validator](/protocol/blockchain/validator/)
in the [committee](/protocol/consensus/committee/).
By committing a sortition transaction, the validator will enter the committee.
Sortition transactions are valid for 7 blocks, which is defined as "sortition interval" in the
[consensus parameters](/protocol/consensus/parameters/).
Sortition is free. This means there are no fees associated with the process of sortition transaction.

## Payload Structure

The sortition transaction has a payload consists the following fields:

| Field           | Size     |
| --------------- | -------- |
| Address         | 21 bytes |
| Sortition Proof | 48 bytes |

- **Address** is the address of the validator that evaluated the sortition
- **Sortition Proof** is the proof of evaluating the sortition

Validators do not need to pay a fee for sortition transactions, and the fee should be set to zero.
