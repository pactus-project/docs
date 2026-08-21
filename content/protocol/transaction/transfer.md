---
title: Transfer Transaction
weight: 2
math: false
---

Transfer transaction is used to transfer coins between the [accounts](/protocol/blockchain/account/).
If the receiver account does not exist, it will be created.

The [Payload Type](/protocol/transaction/format/#payload-type) for Transfer is 1.

## Payload Structure

The transfer transaction has a payload that consists of the following fields:

| Field            | Size     |
| ---------------- | -------- |
| Sender address   | 21 bytes |
| Receiver address | 21 bytes |
| Amount           | Variant  |

- **Sender address** is the account address that transfers the amount
- **Receiver address** is the account address that receives the amount
- **Amount** is the amount of coins that should be transferred

## Reward Transaction

The reward transaction is the first transaction in each block. There is only one reward transaction
per block, and it has zero fees and no signature.

In protocol version 1, the reward transaction had the same format as a transfer transaction.
The sender address was the [Treasury address](/protocol/blockchain/address#treasury-address),
and the receiver address was defined by the block proposer.
The amount of the reward transaction was equal to the
[block reward](/protocol/blockchain/incentive/#block-reward) plus transaction fees,
and the full amount went to the proposer account as a block reward.

Starting with protocol version 2, the reward transaction is a
[batch transfer transaction](/protocol/transaction/batch_transfer) that splits the block reward
according to [PIP-43](https://pips.pactus.org/PIPs/pip-43):
**70%** to the block proposer and **30%** to the Pactus Foundation.
Starting with protocol version 4, the reward amount follows the halving schedule defined by
[PIP-55](https://pips.pactus.org/PIPs/pip-55).
