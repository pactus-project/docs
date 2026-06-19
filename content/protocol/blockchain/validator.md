---
title: Validator
weight: 3
---

A Validator is an entity that participates in the consensus process by sharing its votes.
Validators get rewarded for creating new blocks, and to become a Validator,
they must "bond" or lock up a certain amount of coins as stake.
The amount of stake held by validators determines their power in the consensus.

## Validator Structure

The base Validator structure is 120 bytes long and consists of the following fields:

| Field                | Size     |
| -------------------- | -------- |
| Public Key           | 96 bytes |
| Number               | 4 bytes  |
| Stake                | 8 bytes  |
| Last Bonding Height  | 4 bytes  |
| Unbonding Height     | 4 bytes  |
| Last Sortition Height| 4 bytes  |

- **Public Key** is the Validator's public key.
- **Number** is a sequential and unique number assigned to each validator when it is created for the first time.
  The validator number is used to calculate the [state hash](/protocol/blockchain/state-hash) of the blockchain.
- **Stake** holds the Validator's stake or the amount of Pactus coins locked or "staked" by the Validator.
- **Last Bonding Height** is the last block height at which the validator bonded stake.
- **Unbonding Height** is the block height at which the validator's stake is unbonded.
  If greater than zero, the validator is considered unbonded.
- **Last Sortition Height** is the last block height at which the validator evaluated sortition.

## Delegation (PIP-49)

[PIP-49](https://pips.pactus.org/PIPs/pip-49) introduces an optional delegation section that adds 33 bytes to the structure:

| Field           | Size     |
| --------------- | -------- |
| Delegate Owner  | 21 bytes |
| Delegate Share  | 8 bytes  |
| Delegate Expiry | 4 bytes  |

When the delegation fields are present, the total structure size is 153 bytes.

- **Delegate Owner** is the address of the stake owner account.
- **Delegate Share** is the stake owner's reward share in nano PAC (within `[0, 0.7 PAC]`).
- **Delegate Expiry** is the block height at which the delegation expires (zero means no expiry).
