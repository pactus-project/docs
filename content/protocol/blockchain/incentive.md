---
title: Incentive
weight: 6
---

> The incentive may help encourage nodes to stay honest.
>
> [Satoshi Nakamoto](https://bitcoin.org/bitcoin.pdf)

In Pactus, rewards are given to validators for collecting valid transactions and creating new blocks.
These rewards serve as an incentive for validators to participate in the consensus process and
maintain the security and integrity of the network.

## Flat Reward

To better understand the incentive model in Pactus, let's compare it with the Bitcoin reward model.
This comparison helps to understand how the incentive model works in Pactus.

| Pactus                                 | Bitcoin                                      |
| -------------------------------------- | -------------------------------------------- |
| Consensus engine is Proof of Stake     | Consensus engine is Proof of Work            |
| every 10 seconds one block is _minted_ | Around every 10 minutes one block is _mined_ |
| Total supply is 42,000,000 coins       | Total supply is 21,000,000 coins             |
| Always one coin per block              | Initial block reward is 50 coins             |
| No halving                             | Halving happens every 4 years                |

The halving mechanism in Bitcoin rewards early contributors more significantly.
However, in a Proof-of-Stake blockchain, this mechanism can lead to wealth centralization,
as early validators gain too much power based on their staked coins.

To promote fairer block rewards, Pactus has introduced a simple and straightforward incentive model called the "Flat Reward."
In this model, the total block reward remains constant at one coin per block and does not change over time.

![Rewards in Bitcoin](/images/bitcoin-reward.png)

![Rewards in Pactus](/images/pactus-reward.png)

## Reward Distribution

In Pactus, the reward distribution is linear. This linear distribution is a direct result of the Flat Reward system.
Unlike other blockchains that have a curved distribution, Pactus maintains a consistent reward distribution.

![Reward distribution in Bitcoin](/images/bitcoin-reward-distribution.png)

![Reward distribution in Pactus](/images/pactus-reward-distribution.png)

## Reward Transaction

The reward transaction is a special transaction type that serves as the first transaction in each block.
The reward transaction is similar to the [coinbase transaction in Bitcoin](https://developer.bitcoin.org/reference/transactions.html#coinbase-input-the-input-of-the-first-transaction-in-a-block).
It is the mechanism through which coins from the [Treasury account](/protocol/blockchain/account/#treasury-account) are distributed among validators as compensation for their role in maintaining network security.

### Legacy Reward Transaction

In protocol version 1, the reward transactions used a simple [transfer](/protocol/transaction/transfer) where all block rewards went to the block proposer.

### Split Reward Transaction

Starting with protocol version 2, reward transactions use [batch transfer transactions](/protocol/transaction/batch_transfer) to distribute block rewards according to [PIP-43](https://pips.pactus.org/PIPs/pip-43):

- **70%** to the block proposer
- **30%** to the Pactus Foundation

