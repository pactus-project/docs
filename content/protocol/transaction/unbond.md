---
title: Unbond Transaction
weight: 5
math: false
---

Unbond transaction is used to unbond a [validator](/protocol/blockchain/validator/).
An unbonded validator becomes inactive and can no longer participate in the sortition algorithm.
After 21 days, the stake can be withdrawn.
This period is called the "unbond interval" and is defined in the [consensus parameter](/protocol/consensus/parameters/).
Unbonding is free. This means there are no fees associated with the process of unbond transaction.

The [Payload Type](/protocol/transaction/format/#payload-type) for Unbond is 4.

## Payload Structure

The unbond transaction has a payload that consists of the following field:

| Field             | Size     |
| ----------------- | -------- |
| Validator address | 21 bytes |

- **Validator address** is the address of validator that is unbonded.
