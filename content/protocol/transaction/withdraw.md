---
title: Withdraw Transaction
weight: 7
math: false
---

A withdraw transaction is used to retrieve the staked coins from an unbonded
[validator](/protocol/blockchain/validator/).
If the validator is still in the unbond period, the transaction will be rejected.
The unbond period is a 21-day interval during which the validator is inactive, but their stake cannot yet be withdrawn.

The [Payload Type](/protocol/transaction/format/#payload-type) for Withdraw is 5.

## Payload Structure

The withdraw transaction has a payload consists the following fields:

| Field            | Size     |
| ---------------- | -------- |
| Sender address   | 21 bytes |
| Receiver address | 21 bytes |
| Amount           | Variant  |

- **Sender address** is the address of the unbonded validator.
- **Receiver address** is the address of the receiver [account](/protocol/blockchain/account/).
- **Amount** is the amount of coins that should be withdrawn
