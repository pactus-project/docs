---
title: Running a Pruned Node
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

## Prune Your Full Node

If you are running a Full Node and want to prune its data to operate in pruned mode, follow these steps:

{{% steps %}}

### Stop the Node

Stop your node if it's running.

### Open a Terminal

Open a Terminal or Command Prompt:

- On **macOS/Linux**: Open the **Terminal**.
- On **Windows**: Use **Command Prompt** or **PowerShell**.

### Run the Prune Command

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

### Restart the Node

Start your Pactus node again to resume normal operation.

{{% /steps %}}

This process removes all blocks and transactions older than your configured `store.retention_days`
(default: 10 days). You can adjust it in your node
[config](/get-started/configuration/) if you want to keep more
or less history.
Pruning is especially useful for users with limited storage capacity.

## Importing a Blockchain Snapshot (Pruned Mode)

To get your node up and running quickly, you can import a recent pruned snapshot of the blockchain.
This is much faster than syncing from the genesis block.

{{< callout type="warning" >}}
   Before importing, make sure your node is **completely stopped**.
   Importing while the node is running can corrupt your data.
{{< /callout >}}

### Option 1: Automatic Import (Recommended)

The `import` command automates the process.

{{% steps %}}

#### Stop the Node

Stop your node if it's running.

#### Import the Latest Snapshot

Run the import command:
{{< os_tabs items="unix,windows" >}}
{{< os_tab >}}

```shell
./pactus-daemon import --working-dir=<PATH-TO-WORKING-DIR>
```

{{< /os_tab >}}
{{< os_tab >}}

```shell
./pactus-daemon.exe import --working-dir=<PATH-TO-WORKING-DIR>
```

{{< /os_tab >}}
{{< /os_tabs >}}

*(Replace `<PATH-TO-WORKING-DIR>` with your node's working directory).*

The daemon will automatically download and import
the latest official snapshot from [https://snapshot.pactus.org](https://snapshot.pactus.org).

#### Restart the Node

Start your node normally after the import finishes.

{{% /steps %}}

### Option 2: Manual Import

Use this method if you want to choose a specific snapshot or download it manually.

{{% steps %}}

#### Stop the Node

Stop your node if it's running.

#### Download a Snapshot

Download a snapshot from [https://snapshot.pactus.org](https://snapshot.pactus.org).
Each snapshot shows its creation date, file size, and a SHA256 checksum for verification.

#### Extract the Snapshot

Extract the archive directly into your node's working directory.
The extracted contents should go into the `data` folder inside the working directory (e.g., `~/pactus/data/`).

#### Restart the Node

Start your node normally. It will resume operation from the imported state.

{{% /steps %}}
