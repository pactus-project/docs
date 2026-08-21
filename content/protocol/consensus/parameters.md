---
title: Consensus Parameters
weight: 6
math: false
---

Consensus parameters are a set of configurable settings that determine how the Pactus blockchain operates.
These parameters are agreed upon by all validators in the network,
ensuring that validators behave in the same way and that the network operates consistently.

Here is the list of the consensus parameters:

## Protocol Version

The version number of the blockchain protocol.
The current protocol version is 4 after [PIP-55](https://pips.pactus.org/PIPs/pip-55).

## Block Time

The time interval in seconds between the creation of two consecutive blocks.
This is set to 10 seconds, which means that a new block is created every 10 seconds.

## Committee Size

The number of validators in the committee.
This is set to 51 validators.

## Block Reward

The total block reward minted for each new block.
It follows the halving schedule defined by [PIP-55](https://pips.pactus.org/PIPs/pip-55),
starting at 1,000,000,000 NanoPAC (one PAC coin) and halving at blocks 8,000,000, 24,000,000, and 56,000,000,
with a floor of 125,000,000 NanoPAC (0.125 PAC coin).

## Time-to-Live Interval

The number of blocks that a transaction can remain unprocessed before
it is removed from the transaction pool.
This is set to 8640 blocks, which is almost one day.

## Bond Interval

The minimum number of blocks that must elapse after a validator has submitted a bond transaction
before they can participate in the consensus process and join the validator committee.
This is set to 360 blocks, which is almost one hour.

## Unbond Interval

The minimum number of blocks that must elapse after a validator has submitted
an unbond transaction before
they can withdraw their staked coins.
This is set to 181,440 blocks, which is almost 21 days.

## Sortition Interval

The maximum number of blocks that a sortition transaction can remain valid and be included
in a block.
This is set to 7 blocks.

## Maximum Stake

The maximum amount of coins that can be staked by a validator.
This is set to 1,000,000,000,000 (NanoPAC), which is 1,000 PAC coins.

## Minimum Stake

The minimum amount of coins that can be staked by a validator.
This is set to 1,000,000,000 (NanoPAC), which is 1 PAC coin.
