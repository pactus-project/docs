---
title: Withdraw Transaction
weight: 7
math: false
---

Withdraw transaction is used to withdraw the staked coins from an unbonded
[validator](/protocol/blockchain/validator/)

## Payload Structure

The withdraw transaction has a payload consists the following fields:

| Field            | Size     |
| ---------------- | -------- |
| Sender address   | 21 bytes |
| Receiver address | 21 bytes |
| Amount           | Variant  |

- **Sender address** is the address of the sender validator.
- **Receiver address** is the address of the receiver [account](/protocol/blockchain/account/).
- **Amount** is the amount of coins that should be withdrawn
