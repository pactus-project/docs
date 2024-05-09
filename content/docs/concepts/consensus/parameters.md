---
title: Parameters
weight: 6
math: false
---

Consensus parameters are a set of configurable settings that determine how the Pactus blockchain operates.
These parameters are agreed upon by all validators in the network,
ensuring that validators behave in the same way and that the network operates consistently.

Here is the list of the consensus parameters:

- **Block Version:** The version number of the blockchain protocol.
  This is set to 1.
- **Block Time:** The time interval in seconds between the creation of two consecutive blocks.
  This is set to 10 seconds, which means that a new block is created every 10 seconds.
- **Committee Size** The number of validators in the committee.
  This is set to 51 validators.
- **Block Reward** The fixed reward amount given to the validator who successfully creates and proposes a new block.
  This is set to 1,000,000,000, which is equivalent to one coin.
- **Time-to-Live Interval**: The number of blocks that a transaction can remain unprocessed before
  it is removed from the transaction pool.
  This is set to 8640 blocks, which is almost one day.
- **Bond Interval**: The minimum number of blocks that must elapse after a validator has submitted a bond transaction
  before they can participate in the consensus process and join the validator committee.
  This is set to 360 blocks, which is almost one hour.
- **Unbond Interval**: The minimum number of blocks that must elapse after a validator has submitted
  an unbond transaction before
  they can withdraw their staked coins.
  This is set to 181440 blocks, which is almost 21 days.
- **Sortition Interval**: The maximum number of blocks that a sortition transaction can remain valid and be included
  in a block.
  This is set to 7 blocks.
- **Fee Fraction**: The fraction of transaction value that must be paid in order for a transaction to be included in a block.
  This is set to 0.0001 PAC, meaning that 0.01% of transaction value are awarded to the block proposer.
- **Minimum Fee**: The minimum transaction fee that must be paid.
  This is set to 1,000 (satoshi), which is equivalent to 0.000001 PAC coin.
- **Maximum Fee**: The maximum transaction fee that must be paid.
  This is set to 1,000,000 (satoshi), which is equivalent to 0.001 PAC coin.
- **Maximum Stake**: The maximum amount of coins that can be staked by a validator.
  This is set to 1,000,000,000,000 (satoshi), which is 1000 PAC coins.
- **Minimum Stake**: The minimum amount of coins that can be staked by a validator.
  This is set to 1,000,000,000 (satoshi), which is 1 PAC coins.
```shell
000000   A6 01 01 02 18 64 03 00  04 58 20 19 BA 0A 47 81  ¦....d...X .º.G.
000010   3C 13 B2 45 9F 4C E3 85  1C A4 2D A8 29 9C 4F 17  <.²E.Lã..¤-¨).O.
000020   B2 26 E8 BA D1 A9 85 91  72 AB 96 05 55 01 5D A8  ²&èºÑ©..r«..U.]¨
000030   F5 E1 96 D6 E9 61 60 9A  E4 15 28 C4 EC 73 68 97  õá.Öéa`.ä.(Äìsh.
000040   59 37 06 58 30 B0 47 D5  C2 C0 72 29 92 84 35 5F  Y7.X0°GÕÂÀr)..5_
000050   5B 50 14 B5 BF 77 F1 70  2B C0 8B 36 06 1D DB A0  [P.µ¿wñp+À.6..Û 
000060   8E 41 BE BF 51 AB 04 16  D2 65 97 31 90 D2 6C BB  .A¾¿Q«..Òe.1.Òl»
000070   79 14 46 81 E7                                    y.F.ç
```