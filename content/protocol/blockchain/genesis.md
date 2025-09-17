---
title: Genesis
weight: 5
math: true
---

The Pactus blockchain starts from scratch.
Its starting point is known as the genesis block, which was created by the bootstrap validators on **January 24, 2024**.

## Bootstrapping

The Pactus blockchain started with four _bootstrap_ validators.
These bootstrap validators did not have any stake, however their voting power was set to one within the consensus algorithm.
Their primary role was to initiate the blockchain during a brief period known as the bootstrapping phase.

The bootstrapping phase has been completed. The bootstrap validators have retired, and
the blockchain is now secured by regular validators who have staked coins to participate in the consensus.

### Bootstrap Node Addresses

The four bootstrap validators that initiated the Pactus blockchain are:

- **Bootstrap 1**: [pc1p378jgjtlse3ae528p7zashmlmnwtu4dres9vtw](https://pacviewer.com/address/pc1p378jgjtlse3ae528p7zashmlmnwtu4dres9vtw)
- **Bootstrap 2**: [pc1plq8uyn6en0gj4k8qnh96tnzqjv4cgu49dxtly7](https://pacviewer.com/address/pc1plq8uyn6en0gj4k8qnh96tnzqjv4cgu49dxtly7)
- **Bootstrap 3**: [pc1pm93ykyvcm6kxewn958kvevkxgkr86j0t6n0aa4](https://pacviewer.com/address/pc1pm93ykyvcm6kxewn958kvevkxgkr86j0t6n0aa4)
- **Bootstrap 4**: [pc1pp3xtmjhzhg36xv6ln9824ugy5n6nnqdzugzu3j](https://pacviewer.com/address/pc1pp3xtmjhzhg36xv6ln9824ugy5n6nnqdzugzu3j)

## Genesis Block

The [genesis block](https://pacviewer.com/block/1) is
the first [block](/protocol/blockchain/block/) in the Pactus blockchain,
and it was created by the bootstrap validators.
This block marked the beginning of the blockchain and serves as the foundation for subsequent blocks.

The previous [block hash](/protocol/blockchain/block/#block-hash) in the genesis block is set to 0,
indicating that it has no predecessor.
Additionally, the genesis block does not have a previous certificate.

## Genesis Information

In Pactus, the Genesis Information was pre-defined and indicated the initial state of the network.
These parameters are hardcoded into the project and include:

- **Genesis Time** The genesis block was created on January 24, 2024, at 20:24:00 UTC.
  This marked the official launch of the Pactus mainnet. The bootstrap validators were operational before this time.
- **Consensus Parameters**: The initial [consensus parameters](/protocol/consensus/parameters)
  were defined at genesis time and ensure that the entire network operates within the same configuration.
  These consensus parameters are discussed in detail in the consensus section of the documentation.
- **Treasury Account**: The [treasury account](/protocol/blockchain/account/#treasury-account)
  held 21 million coins at the genesis time. Each coin is divided into 1 billion units (NanoPAC).
- **Reserved Accounts**: Reserved accounts were defined at the Genesis time and have a total of 21 million coins.
  These coins are reserved and the main purpose is to support the project over time.
- **Bootstrap Validators**: The bootstrap validators were defined by their public keys and
  were responsible for creating the genesis block.

## FAQ

### Where can I see the Genesis Information?

You can find the Genesis Information of the Pactus blockchain in the `genesis.json` file,
which is located in the project repository,
[here](https://github.com/pactus-project/pactus/blob/main/genesis/mainnet.json).

### What happened to the bootstrap validators?

The bootstrap validators completed their role in securing the network during the initial bootstrapping phase.
They have since retired, and the network is now secured by regular validators who
have staked coins to participate in the consensus mechanism.

### How many coins were allocated at genesis?

At genesis time, the total coin allocation was:

- **Treasury Account**: 21 million coins
- **Reserved Accounts**: 21 million coins
- **Total**: 42 million coins

Each coin is divided into 1 billion units (NanoPAC), making the total supply **42 billion NanoPAC**.
It means
$$ 1 \text{ PAC} = 10^9 \text{ NanoPAC} $$

### When exactly was the Pactus blockchain launched?

The Pactus mainnet was officially launched on **January 24, 2024, at 20:24:00 UTC**.
This timestamp represents the creation of the genesis block and marks the beginning of the Pactus blockchain.

### What is the significance of the genesis block?

The genesis block serves as the foundation of the entire Pactus blockchain. It:

- Marks the official launch of the network
- Establishes the initial state and parameters
- Provides the starting point for all subsequent blocks
- Contains no previous block hash (set to 0)
- Has no previous certificate
