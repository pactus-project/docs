---
title: Solid State Proof of Stake
weight: 1
---

## Proof of Stake

Proof of Stake is a method used to keep a blockchain network secure and running smoothly.
Instead of using a lot of computer power to solve complex puzzles (like in Proof of Work),
Proof of Stake asks users to put some of their coins at stake.
These users, known as validators, verify and add new transactions to the blockchain.
In return, they earn extra coins as a reward.

Unlike Proof of Work, which is based on competition, Proof of Stake is based on collaboration.
Validators work together to manage the expansion of the blockchain.
A Proof of Stake blockchain becomes more decentralized and secure as more validators participate in it.

### Community Bank Example

To understand how Proof of Stake works, think of a community bank run by its members without a central authority.
The members decide to manage the bank together.
Some members volunteer to collect, check, and record transactions to keep everything running smoothly.

These volunteers, known as validators, must temporarily lock up some of their money as a stake.
This staked money can’t be moved or used.
The more money a validator stakes, the more influence they have in the system.

From time to time, one of the validators is chosen by the others to collect all the recent transactions,
bundle them together, and send a copy to the other validators.
If a supermajority of the validators agree with the proposed bundle by signing it,
the bundle will be committed to the bank's ledger.

In this system, validators are encouraged to act honestly.
If they don’t, they risk damaging the bank’s reputation and losing the value of their staked money.

## Delegated Proof of Stake

In Proof of Stake, if the number of validators increases,
the voting time will also increase, and this makes the consensus process less efficient.
In our community bank example, running the bank becomes more difficult as the number of validators increases.

To address this problem, some blockchains use the concept of "delegators".
In Delegated Proof of Stake, users entrust their stakes to a small group of "delegates".
These delegates are responsible for validating transactions and creating blocks.
The number of delegates is limited to ensure accountability and efficiency in the validation process.

![Delegated Proof of Stake](/images/delegated-proof-of-stake.png)

The delegation model puts a lot of trust in the hands of a small number of delegates,
which goes against the principle of "don't trust, verify".

## Solid State Proof of Stake (SSPoS)

Pactus introduced a new mechanism called Solid State Proof of Stake that operates without delegation.
It employs a dynamic [committee](/protocol/consensus/committee/) of validators that are responsible for creating new blocks.
The size of the committee is fixed, but the members of the committee are randomly changed.
On the other hand, the number of validators outside the committee is unlimited, allowing anyone to
become a validator by staking coins.

At each block, validators participate in a [sortition](/protocol/consensus/sortition/) algorithm
by generating a random number between zero and the total staked coins.
If the number is less than the validator's stake, they can enter the committee and replace the oldest committee member.

![Pactus Solid State Proof of Stake](/images/pactus-solid-state-proof-of-stake.png)

The chance of entering the committee depends on the validator's stake and luck.
But on average, one validator should enter the committee in each block.
