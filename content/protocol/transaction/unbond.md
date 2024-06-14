---
title: Unbond Transaction
weight: 6
math: false
---

Unbond transaction is used to unbond a [validator](/protocol/blockchain/validator/).
An unbonded validator cannot participate in the sortition algorithm anymore, and after 21 days, the stake can be withdrawn.
This is called the "unbond interval" and is defined in the [consensus parameter](/protocol/consensus/parameters/).

## Payload Structure

The unbond transaction has a payload consists the following field:

| Field             | Size     |
| ----------------- | -------- |
| Validator address | 21 bytes |

- **Validator address** is the address of validator that is unbonded.
