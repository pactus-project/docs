---
title: Run Pactus in Graphic Mode
weight: 2
---

## Preface

Pactus can be run in different modes, including the command-line interface (CLI) and the graphical user interface (GUI).
This tutorial will guide you through the steps to run Pactus in GUI mode, suitable for beginner to advanced users.

## Prerequisites

Before proceeding with the steps below, ensure that you have the following:

- A computer running Windows, macOS, or Linux
- Suitable internet connection

## Download

Download the Pactus GUI installer or archived file from
[here](https://pactus.org/download/#gui).

## Installing

To install Pactus GUI, simply follow the on-screen instructions provided by the installer.
The process is straightforward and similar to installing any other application on your computer.

![Installing Pactus](/images/pactus-gui/installing.png)

## Initializing

When you run Pactus for the first time, a wizard dialog will appear to guide you through the wallet creation and
initialization process. This process consists of several steps:

### Wallet Mode

On the first page, you will ask you how you want to create your wallet.
Select the option to "Create a new wallet from scratch" and proceed to the next page.

![Initialize mode](/images/pactus-gui/wallet-mode.png)

### Wallet Seed

The next page will display your wallet seed phrase, which consists of 12 words.
It is essential to securely back up this seed phrase, as it is required for wallet recovery
in case your computer is lost, damaged, or stolen.

![Wallet seed](/images/pactus-gui/wallet-seed.png)

{{< callout type="warning" >}}
 <b>Wallet seed is important</b>
      <br><br>
Keep your wallet seed phrase private and secure.
If someone else gains access to your seed phrase, they can control your wallet and funds.
{{< /callout >}}

### Seed Confirmation

In this step, you will be asked to confirm your seed phrase.
Input the 12 words you received in the previous step into the dialog.
If the seed phrase is entered correctly, you will be able to proceed to the next page.

![Seed confirmation](/images/pactus-gui/seed-confirmation.png)

### Wallet Password

On this page, you will be asked to set a password for your wallet.
Enter a strong password in the first dialog box and confirm it in the second one.
This password will be used to encrypt your wallet and protect it from unauthorized access.

![Set wallet password](/images/pactus-gui/wallet-password.png)

Note: Choose a strong password and keep it safe.
If you forget or lose your password, you will need your seed phrase to regain access to your wallet.

### Number of Validators

Each node in the Pactus blockchain can run up to 32 validators, and each validator can stake up to
1000 coins. Here, you can define how many validators you want to create for your node.
Select the number of validators based on the amount of coins you want to stake.

![Number of Validators](/images/pactus-gui/number-of-validators.png)

If you want to stake more than 32,000 coins, you need to set up a new node.

### Node Type

On this page, you to choose the mode in which your node will operate: **Pruned Mode** or **Full Mode**.

![Node Type](/images/pactus-gui/node-type.png)

Starting with version 1.4.0, Pactus supports Pruned Mode.
In this mode, you don't need to download the entire blockchain;
instead, you can download recent blocks from the last 10 days.
This significantly speeds up the syncing process.

### Summary

The last page of the initialization process shows the node information, such as the working directory, validator address,
and reward address. Review this information and click "Close" to complete the initialization process.

![Summary](/images/pactus-gui/summary.png)

Upon closing the wizard dialog, your Pactus node will start running. You are now ready to use Pactus in GUI mode.

## Running the Pactus Node

After completing the initialization process, you are ready to run the Pactus node.
Running a Pactus node allows you to synchronize with the network, enabling you to manage your wallet and
sending transactions.

### Syncing with the Network

When the Pactus node starts running, it begins syncing with the network. This process may take some time,
as your node needs to download and verify the blockchain.

![Syncing progress](/images/pactus-gui/syncing-progress.png)

### Default Wallet

You can check the "Default Wallet" tab to access your wallet information. Please note that the displayed
information may not be accurate until the syncing process is complete.

![Default Wallet tab](/images/pactus-gui/default-wallet.png)

In the "Default Wallet" tab, you can view your account details, including your balance and
address information such as the **validator and reward addresses**.
Your computer acts as a node and is recognized by the validator address in the Pactus network.
The reward address is the account address where you collect the
[rewards](/protocol/blockchain/incentive/) earned by participating in
the consensus algorithm and proposing new blocks.

By running a Pactus node, you contribute to the decentralization and security of the Pactus blockchain network.
Thank you for your participation!
