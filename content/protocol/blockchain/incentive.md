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

## Block Reward

To better understand the incentive model in Pactus, let's compare it with the Bitcoin reward model.
This comparison helps to understand how the incentive model works in Pactus.

| Pactus                                        | Bitcoin                                      |
| --------------------------------------------- | -------------------------------------------- |
| Consensus engine is Proof of Stake            | Consensus engine is Proof of Work            |
| every 10 seconds one block is _minted_        | Around every 10 minutes one block is _mined_ |
| Genesis supply is 42,000,000 coins            | Total supply is 21,000,000 coins             |
| Reward starts at one coin per block           | Initial block reward is 50 coins             |
| Halving at blocks 8M, 24M, and 56M            | Halving happens every 4 years                |
| Reward floor is 0.125 coins per block         | No reward floor (reward tends to zero)       |

Pactus initially used a "Flat Reward" model with a constant reward of one coin per block.
This simple model was fair, but it created an unbounded linear supply with no long-term issuance discipline.

To limit supply and give the network time to adapt, [PIP-55](https://pips.pactus.org/PIPs/pip-55)
introduced a block reward halving schedule.
The reward starts at 1 PAC per block and is halved three times with doubling intervals:

| Start block | End block  | Reward per block | Total blocks | Total PAC |
| ----------- | ---------- | ---------------- | ------------ | --------- |
| 1           | 8,000,000  | 1.000 PAC        | 8,000,000    | 8,000,000 |
| 8,000,001   | 24,000,000 | 0.500 PAC        | 16,000,000   | 8,000,000 |
| 24,000,001  | 56,000,000 | 0.250 PAC        | 32,000,000   | 8,000,000 |
| 56,000,001  | —          | 0.125 PAC        | —            | —         |

After the third halving at block 56,000,000, the reward remains at 0.125 PAC per block.

![Rewards in Bitcoin](/images/bitcoin-reward.png)

![Rewards in Pactus](/images/pactus-reward.png)

## Reward Distribution

In Pactus, the reward distribution is piecewise linear.
Within each halving era, the total amount of distributed coins grows linearly,
but the slope is halved at each halving boundary, resulting in a decreasing issuance curve.

![Reward distribution in Bitcoin](/images/bitcoin-reward-distribution.png)

![Reward distribution in Pactus](/images/pactus-reward-distribution.png)

## Reward Transaction

The reward transaction is a special transaction type that serves as the first transaction in each block.
The reward transaction is similar to the
[coinbase transaction in Bitcoin](https://developer.bitcoin.org/reference/transactions.html#coinbase-input-the-input-of-the-first-transaction-in-a-block)
. It is the mechanism through which coins from the
[Treasury account](/protocol/blockchain/account/#treasury-account)
are distributed among validators as compensation for their role in maintaining network security.

### Legacy Reward Transaction

In protocol version 1, the reward transactions used a simple
[transfer](/protocol/transaction/transfer) where all block rewards went to the block proposer.

### Split Reward Transaction

Starting with protocol version 2, reward transactions use
[batch transfer transactions](/protocol/transaction/batch_transfer)
to distribute block rewards according to [PIP-43](https://pips.pactus.org/PIPs/pip-43):

- **70%** to the block proposer
- **30%** to the Pactus Foundation

Starting with protocol version 4, the amount distributed by the reward transaction follows the
halving schedule defined in [PIP-55](https://pips.pactus.org/PIPs/pip-55).
The split between the block proposer and the Pactus Foundation remains unchanged at **70/30**.
