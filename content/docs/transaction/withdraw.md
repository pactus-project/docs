---
title: Withdraw Transaction
weight: 7
math: false
---

Withdraw transaction is used to withdraw the staked coins from an unbonded
[validator](/docs/blockchain/validator/)

## Payload Structure

The withdraw transaction has a payload consists the following fields:

| Size     | Field            |
| -------- | ---------------- |
| 21 bytes | Sender address   |
| 21 bytes | Receiver address |
| Variant  | Amount           |

- **Sender address** is the address of the sender validator.
- **Receiver address** is the address of the receiver [account](/docs/blockchain/account/).
- **Amount** is the amount of coins that should be withdrawn
