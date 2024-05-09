---
title: Transfer Transaction
weight: 3
math: false
---

Transfer transaction is used to transfer coins between the [accounts](/docs/concepts/blockchain/account/).
If the receiver account does not exist, it will be created.

## Payload Structure

The transfer transaction has a payload consists the following fields:

| Size     | Field            |
| -------- | ---------------- |
| 21 bytes | Sender address   |
| 21 bytes | Receiver address |
| Variant  | Amount           |

- **Sender address** is the account address that transfers the amount
- **Receiver address** is the account address that receives the amount
- **Amount** is the amount of coins that should be transferred

## Reward Transaction

The reward transaction is the first transaction in each block. There is only one reward transaction
per block, and it has the same format as a transfer transaction, but with zero fees and no signature.

The sender address is the [Treasury address](/docs/concepts/blockchain/address#treasury-address),
and the receiver address is defined by the block proposer.
The amount of the reward transaction should be equal to the
[block reward](/docs/concepts/blockchain/incentive/#flat-reward) plus transaction fees.
This amount will go to the proposer account as a block reward.
Therefore, in each block, one coin from the
[Treasury account](/docs/concepts/blockchain/account#treasury-account) transfers to
the proposer account as a block reward.
