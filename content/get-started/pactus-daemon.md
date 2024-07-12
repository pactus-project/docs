---
title: Run Pactus in Command Line Mode
weight: 3
---

## Preface

Pactus can be run in different modes, including the command-line interface (CLI) and the graphical user interface (GUI).
This tutorial will guide you through the steps to run Pactus in CLI mode, suitable for advanced users.

## Prerequisites

Before proceeding with the steps below, ensure that you have the following:

- A computer running Windows, macOS, or Linux
- Suitable internet connection

## Download

To get started, download and extract the Pactus CLI file from
[here](https://pactus.org/download/#cli).
Once you have downloaded and extracted the Pactus CLI file, you can proceed to the next step.

## Initializing the Node

Now you need to create a wallet and setup a working directory for your node.
A working directory is a place where you save blockchain data and wallets.
Open the Terminal and run the following command:

{{< tabs items="Linux-mac,windows" >}}
  {{< tab >}}

```bash
./pactus-daemon init
```

This command creates your wallet and setup the working directory at `~/pactus`.
  {{< /tab >}}
  {{< tab >}}

```powershell
pactus-daemon.exe init
```

This command creates your wallet and setup the working directory at `C:\Users\<USER_NAME>\pactus`.
  {{< /tab >}}
{{< /tabs >}}

{{< callout type="info" >}}
<b>Working director</b>
<br><br>
By default the working directory that store the blockchain data stores in `~/pactus` in Unix-like systems.
For Windows it stores in `C:\Users\<USER_NAME>\pactus`.
<br><br>
If you wish to select or specify a different path, use the `--working-dir` option.
{{< /callout >}}

{{< callout type="warning" >}}
<b>Wallet seed is important</b>
      <br><br>
      Keep your wallet seed phrase private and secure.
      If someone else gains access to your seed phrase, they can control your wallet and funds.
{{< /callout >}}

The working directory contains:

- Default wallet
- Genesis file
- Config file

Feel free to explore the contents of these files as needed, particularly the config file.
The config file contains parameters that can customize your node.

### Restoring the Node

If you ever need to restore your node, for instance on a new device,
you can use the `--restore` option followed by your mnemonic:

{{< tabs items="Linux-mac,windows" >}}
  {{< tab >}}

```bash
./pactus-daemon init --restore "<your-mnemonic>"
```

Replace `<your-mnemonic>` with your previously noted mnemonic phrase.
This command will restore your wallet in the `~/pactus` directory.

  {{< /tab >}}
  {{< tab >}}

```powershell
pactus-daemon.exe init --restore "<your-mnemonic>"
```

Replace `<your-mnemonic>` with your previously noted mnemonic phrase.
This command will restore your wallet in the `C:\Users\<USER_NAME>\pactus` directory.
  {{< /tab >}}
{{< /tabs >}}

## Running the Node

Now you can start the node and sync with the network. Run the following command in the Terminal:

{{< tabs items="Linux-mac,windows" >}}
  {{< tab >}}

```bash
./pactus-daemon start
```

  {{< /tab >}}
  {{< tab >}}

```powershell
pactus-daemon.exe start
```

  {{< /tab >}}
{{< /tabs >}}

{{< hextra/hero-button text="How to run Pactus with systemd linux?" link="/tutorials/linux-systemd/" >}}

When the Pactus node starts running, it begins syncing with the network.
This process may take some time, as your node needs to download and verify the entire blockchain history.
Please be patient while your node syncs.

### Default Ports

The default network ports in Pactus are defined as follows.
It is not recommended to change these default ports:

- [P2P](https://libp2p.io/) port is `21888`. P2P supports both UDP and TCP protocols.
- [gRPC](https://grpc.io/) port is `50051`. The gRPC module is enabled by default for localhost.
- [gRPC-gateway](https://grpc-ecosystem.github.io/grpc-gateway/) port is `8080`. The gRPC-gateway is disabled by default.
- [JSON-RPC](https://www.jsonrpc.org/) port is `8545`. The JSON-RPC service is disabled by default.
- [Nanomsg](https://nanomsg.org/) port is `40899`. The Nanomsg service is disabled by default.

## Running Pactus in the Background

To run Pactus commands in the background and keep them running even after you close your terminal or
log out, you can use terminal multiplexer software.
Terminal multiplexers allow you to create and manage multiple terminal sessions within a single window.

Two popular terminal multiplexer options are:

1. **tmux**: [Tmux](https://github.com/tmux/tmux/wiki) is a terminal multiplexer that
2. lets you create, manage, and detach terminal sessions.
3. You can install tmux on Unix-like systems using your package manager (e.g., `apt`, `brew`, `yum`).

   Here's how to use tmux to run Pactus in the background:

   - Start a new tmux session: `tmux`
   - Run your Pactus command within the tmux session.
   - Detach from the tmux session: Press `Ctrl-b`, followed by `d`.
   - Reattach to the tmux session later to check the progress: `tmux attach-session`

4. **screen**: [GNU Screen](https://www.gnu.org/software/screen/) is another terminal multiplexer that
5. allows you to run terminal sessions in the background.

   Here's how to use screen to run Pactus in the background:

   - Start a new screen session: `screen`
   - Run your Pactus command within the screen session.
   - Detach from the screen session: Press `Ctrl-a`, followed by `d`.
   - Reattach to the screen session later to check the progress: `screen -r`

Choose the terminal multiplexer that suits your preference and install it using your system's package manager.
With these tools, you can run Pactus commands in the background with ease.
