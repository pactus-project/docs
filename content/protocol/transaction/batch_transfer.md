---
title: Batch Transfer Transaction
weight: 7
math: false
---

Batch transfer transaction is used to transfer coins to multiple recipients in a single transaction.
This is more efficient than creating multiple individual transfer transactions.
It follows a one-to-many pattern, allowing a single sender to transfer coins to multiple recipients in one transaction.

If any receiver account does not exist, it will be created automatically.

The [Payload Type](/protocol/transaction/format/#payload-type) for Batch Transfer is 6.

## Payload Structure

The batch transfer transaction has a payload that consists of the following fields:

| Field                | Size     |
| -------------------- | -------- |
| Sender address       | 21 bytes |
| Number of Recipients | Variant  |
| Recipients Address 1 | 21 bytes |
| Recipients Amount 1  | Variant  |
| ...                  | ...      |
| Recipients Address N | 21 bytes |
| Recipients Amount N  | Variant  |

- **Sender address** is the account address that transfers the amounts
- **Number of Recipients** specifies how many recipients will receive funds in this transaction (maximum 8 recipients)
- **Recipients Address 1 to N** are the account addresses that receive the amounts
- **Recipients Amount 1 to N** are the amounts of coins that should be transferred to each corresponding recipient

The payload structure allows for up to 8 recipients, with each recipient having a corresponding address and amount pair.
