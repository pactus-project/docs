---
title: How to use Prune Node?
weight: 4
---

## Preface

The Pactus Blockchain supports pruned nodes to help users manage storage efficiently by retaining only
the most recent and relevant data. This tutorial will guide you step-by-step on how to prune your node,
whether using the command line or the graphical interface.

## What is a Pruned Node?

In the context of blockchain, a "pruned node" refers to a type of node that retains
only a certain portion of the blockchain history, rather than the entire ledger.
This is achieved by deleting old transaction data while maintaining the most recent and relevant blocks.
This selective data retention allows nodes to operate without the need for extensive storage,
enabling more participants to run nodes and contribute to network security and decentralization.

## Key Features of Pruned Nodes

1. **Storage Efficiency**: A primary advantage of pruned nodes is their reduced storage footprint.
   This makes it feasible for users with limited hardware resources to run a node, thus increasing
   the overall accessibility and decentralization of the network.

2. **Faster Synchronization**: Because pruned nodes do not require the entire blockchain history,
   they can sync with the Pactus network faster than full nodes. This facilitates quicker participation
   in consensus and transaction validation.

3. **Maintained Security**: Despite lacking full transaction history, pruned nodes still maintain enough
   data to validate current transactions effectively. Therefore, they can participate in consensus
   mechanisms without compromising network security.

4. **Increased Participation**: By lowering the barriers to entry, pruned nodes can significantly
   encourage more users to participate in staking and validating transactions, contributing to
   a more robust and decentralized network.

## Benefits of Pruned Solid State Proof of Stake Nodes

1. **Scalability**: As the Pactus network grows, the size of the blockchain can become cumbersome.
   Pruned nodes help mitigate this issue, allowing Pactus to scale efficiently without overwhelming infrastructure.

2. **Energy Efficiency**: Coupled with the inherent efficiencies of Solid State Proof Of Stake, pruned nodes further
3. reduce the environmental impact of Pactus operations. With fewer resources required for storage and data processing,
   the Pactus network can operate more sustainably.

4. **Enhanced Decentralization**: The ability for more participants to run nodes increases the decentralization of the network.
   A more decentralized network is generally more resilient to attacks and manipulation, which bolsters the integrity
   of the blockchain.

5. **User Empowerment**: Pruned nodes empower users by making it easier for them to participate actively in the Pactus
   ecosystem without needing significant technical expertise or substantial hardware investment.

## Prune Your Full Node

1. **Stop the Running Node**
   Shut down your currently running Pactus full node completely.

2. **Open a Terminal or Command Prompt**
   - On **macOS/Linux**: Open the **Terminal**.
   - On **Windows**: Use **Command Prompt** or **PowerShell**.

3. **Prune the Node Data**
   Run the following command, replacing `<PATH-TO-WORKING-DIR>` with the actual path to your working directory:

{{< os_tabs items="unix,windows" >}}
  {{< os_tab >}}

```bash
./pactus-daemon prune -w <PATH-TO-WORKING-DIR>
```

  {{< /os_tab >}}
  {{< os_tab >}}

```cmd
pactus-daemon.exe prune -w <PATH-TO-WORKING-DIR>
```

  {{< /os_tab >}}
{{< /os_tabs >}}

4. **Restart the Node**
   Start your Pactus node again to resume normal operation.
