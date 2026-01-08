---
title: Join Pactus Testnet
weight: 13
---

## Preface

The Pactus testnet is a public testing environment that replicates the
functionality of the mainnet but uses test coins with no real-world value.
Running a node on the testnet allows you to experiment safely, test applications,
and support the stability of the network.
It also helps the development team test and improve Pactus more effectively.

This document provides a step-by-step guide on how to join the Pactus testnet.

## Set up the node

To set up a Testnet node, first [download](https://pactus.org/download/) the latest version of Pactus.
The Testnet uses the same software as the Mainnet, but it must be configured to connect to the Testnet.

### Running Testnet with Pactus Daemon (CLI)

You can also use the [Pactus Daemon (CLI)](https://docs.pactus.org/get-started/pactus-daemon) to join the Testnet.
To join the Testnet, you need to explicitly specify the `--testnet` flag when initializing the node:

{{< os_tabs items="unix,windows" >}}
  {{< os_tab >}}

```bash
./pactus-daemon init --working-dir=~/pactus/testnet --testnet
```

This command creates your wallet and sets up the working directory at `~/pactus/testnet`.
  {{< /os_tab >}}
  {{< os_tab >}}

```batch
pactus-daemon.exe init --working-dir=%USERPROFILE%\pactus\testnet --testnet
```

This command creates your wallet and sets up the working directory at `C:\Users\<USER_NAME>\pactus\testnet`.
  {{< /os_tab >}}
{{< /os_tabs >}}

Here’s what the flags mean:

- `--working-dir`: Specifies the directory where node data (e.g., blockchain data, configuration files) will be stored.
- `--testnet`: Configures the node to connect to the Testnet instead of the Mainnet.

After initializing the node, you can optionally import the latest blockchain data and
run the Testnet in [pruned mode](https://docs.pactus.org/tutorials/pruned-nodes/).
This helps you sync faster and reduces storage usage:

{{< os_tabs items="unix,windows" >}}
  {{< os_tab >}}

```bash
./pactus-daemon import --working-dir=~/pactus/testnet
```

  {{< /os_tab >}}
  {{< os_tab >}}

```batch
pactus-daemon.exe import --working-dir=%USERPROFILE%\pactus\testnet
```

  {{< /os_tab >}}
{{< /os_tabs >}}

Now, start the node:

{{< os_tabs items="unix,windows" >}}
  {{< os_tab >}}

```bash
./pactus-daemon start --working-dir=~/pactus/testnet

```

  {{< /os_tab >}}
  {{< os_tab >}}

```batch
pactus-daemon.exe start --working-dir=%USERPROFILE%\pactus\testnet
```

  {{< /os_tab >}}
{{< /os_tabs >}}

This command starts your node and connects it to the Pactus Testnet.

### Running Testnet with Pactus GUI

You can also run the Testnet using the [Pactus GUI](https://docs.pactus.org/get-started/pactus-gui).
Open a terminal (or command prompt on Windows) and start Pactus GUI with:

{{< os_tabs items="unix,windows" >}}
  {{< os_tab >}}

```bash
./pactus-gui -working-dir=~/pactus/testnet -testnet
```

  {{< /os_tab >}}
  {{< os_tab >}}

```batch
pactus-gui.exe start -working-dir=%USERPROFILE%\pactus\testnet -testnet
```

  {{< /os_tab >}}
{{< /os_tabs >}}

The GUI will initialize and connect to the Testnet using the specified working directory.

## Obtaining Test Coins

To interact with the Pactus Testnet, you will need test coins (`tPAC`).
These coins have no real-world value but are required for testing transactions,
applications, and validator operations.
You can request up to `5 tPAC` per day from the [Pagu](https://pagu.bot) Project faucet,
which is a convenient way to experiment with your projects or applications.

If you intend to run a validator on the Testnet permanently,
you can reach out to the Pactus team to receive stake coins for your validator.
