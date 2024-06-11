---
title: How to use wallet in Command Line Mode?
weight: 1
---

## Preface

The Pactus Blockchain provides a wallet application that allows users to interact with the Pactus blockchain
without the need to run a node.
This is ideal for users who do not wish to operate a node but still want to create a personal wallet to manage their funds.
This tutorial will guide you step-by-step on how to use the wallet application.

## Download

To get started, download and extract the Pactus CLI file from
[here](https://pactus.org/download/#cli).
Once you have downloaded and extracted the Pactus CLI file, you can proceed to the next step.

## Wallet Commands

In this section, we will explore various wallet commands that help you create, manage,
and recover your Pactus wallet.

<callout type="info">

<b>Wallet Path</b>
<br><br>
By default, the node's wallet is stored at `~/pactus/wallets/default_wallet` on Unix-like systems.
On Windows, you can find it at `C:\Users\<USER_NAME>\pactus\wallets\default_wallet`.
<br><br>
If you wish to select or specify a different wallet, use the `--path` option.
</callout>

### Create a Wallet

To create a new wallet, run the following command:

{{< tabs items="Linux-mac,windows" >}}

  {{< tab >}}
```shell
./pactus-wallet --path <PATH-To-NEW-WALLET> create
```
  {{< /tab >}}

   {{< tab >}}
```shell
pactus-wallet.exe --path <PATH-To-NEW-WALLET> create
```
  {{< /tab >}}
{{< /tabs >}}

Replace `<PATH-To-NEW-WALLET>` with the file path where you want to create the wallet.

### Recover Wallet

If you lose your wallet or forget your password, you can recover it by running this command:


{{< tabs items="Linux-mac,windows" >}}

  {{< tab >}}
```shell
./pactus-wallet --path <PATH-To-NEW-WALLET> recover
```
  {{< /tab >}}

   {{< tab >}}
```shell
pactus-wallet.exe --path <PATH-To-NEW-WALLET> recover
```
  {{< /tab >}}
{{< /tabs >}}

Replace `<PATH-To-NEW-WALLET>` with the file path where you want to restore the wallet.

### Wallet Password

You can change the wallet password by running this command:

{{< tabs items="Linux-mac,windows" >}}

  {{< tab >}}
```shell
./pactus-wallet password
```
  {{< /tab >}}

   {{< tab >}}
```shell
pactus-wallet.exe password
```
  {{< /tab >}}
{{< /tabs >}}

This command changes the password for the `default_wallet` if there is one, or sets a new password.

### Wallet Seed

You can obtain the wallet seed by running this command:

{{< tabs items="Linux-mac,windows" >}}

  {{< tab >}}
```shell
./pactus-wallet seed
```
  {{< /tab >}}

   {{< tab >}}
```shell
pactus-wallet.exe seed
```
  {{< /tab >}}
{{< /tabs >}}

The wallet seed is encrypted within your wallet, and
you'll need to enter the wallet password to access it.

## Address Commands

In this section, we'll cover address commands that help you manage your wallet addresses.

### Creating New Address

You can create a new address by running this command:

{{< tabs items="Linux-mac,windows" >}}

  {{< tab >}}
```shell
./pactus-wallet address new
```
  {{< /tab >}}

   {{< tab >}}
```shell
pactus-wallet.exe address new
```
  {{< /tab >}}
{{< /tabs >}}

Based on [PIP-8](https://pips.pactus.org/PIPs/pip-8), an address string conducts its type and usage.
By default, the above command creates an account address.
If you want to create a validator address instead, you can use the `--type validator` option with the command like this:

{{< tabs items="Linux-mac,windows" >}}

  {{< tab >}}
```shell
./pactus-wallet address new --type validator
```
  {{< /tab >}}

   {{< tab >}}
```shell
pactus-wallet.exe address new --type validator
```
  {{< /tab >}}
{{< /tabs >}}

You can also assign a label to your address to better organize your address book.

### List of Addresses

To view the list of wallet addresses, use this command:

{{< tabs items="Linux-mac,windows" >}}

  {{< tab >}}
```shell
./pactus-wallet address all
```
  {{< /tab >}}

   {{< tab >}}
```shell
pactus-wallet.exe address all
```
  {{< /tab >}}
{{< /tabs >}}

### Get Public Key

To obtain the public key for a specific address, run this command:

{{< tabs items="Linux-mac,windows" >}}

  {{< tab >}}
```shell
./pactus-wallet address pub <ADDRESS>
```
  {{< /tab >}}

   {{< tab >}}
```shell
pactus-wallet.exe address pub <ADDRESS>
```
  {{< /tab >}}
{{< /tabs >}}

Replace `<ADDRESS>` with the address for which you want to retrieve its public key.

### Get Private Key

You can get the private key of your address by this command:

{{< tabs items="Linux-mac,windows" >}}

  {{< tab >}}
```shell
./pactus-wallet address priv <ADDRESS>
```
  {{< /tab >}}

   {{< tab >}}
```shell
pactus-wallet.exe address priv <ADDRESS>
```
  {{< /tab >}}
{{< /tabs >}}

Replace `<ADDRESS>` with the address for which you want to retrieve its private key.
Keep your private key secure. If someone gains access to your private key,
they will have full control over that address.

### Get Address Balance

You can get the balance of your address by this command:

{{< tabs items="Linux-mac,windows" >}}

  {{< tab >}}
```shell
./pactus-wallet address balance <ADDRESS>
```
  {{< /tab >}}

   {{< tab >}}
```shell
pactus-wallet.exe address balance <ADDRESS>
```
  {{< /tab >}}
{{< /tabs >}}

Replace `<ADDRESS>` with the address for which you want to retrieve your balance.

---

## Transaction Commands

In this section, we'll cover transaction commands that help you create, sign, and
broadcast transactions on the Pactus Blockchain.
You'll need to provide the password to sign the transaction.
Please note that once a transaction is broadcasted, it cannot be reversed.

### Sending Transfer Transaction

To create, sign, and broadcast a
[Transfer transaction](/docs/concepts/transaction/transfer/), use the following command:

{{< tabs items="Linux-mac,windows" >}}

  {{< tab >}}
```shell
./pactus-wallet tx transfer <FROM> <TO> <AMOUNT>
```
  {{< /tab >}}

   {{< tab >}}
```shell
pactus-wallet.exe tx transfer <FROM> <TO> <AMOUNT>
```
  {{< /tab >}}
{{< /tabs >}}

In this command, `<FROM>` should be one of the addresses in your wallet as the sender address,
and `<TO>` is the receiver address.

### Sending Bond Transaction

To create, sign, and broadcast a
[Bond transaction](/docs/concepts/transaction/bond/), use the following command:

{{< tabs items="Linux-mac,windows" >}}

  {{< tab >}}
```shell
./pactus-wallet tx bond <FROM> <TO> <AMOUNT>
```
  {{< /tab >}}

   {{< tab >}}
```shell
pactus-wallet.exe tx bond <FROM> <TO> <AMOUNT>
```
  {{< /tab >}}
{{< /tabs >}}

In this command, `<FROM>` should be one of the addresses in your wallet as the sender address,
and `<TO>` is the receiver validator address.

If the validator associated with this address does not exist yet,
you need to provide the public key to create it:

{{< tabs items="Linux-mac,windows" >}}

  {{< tab >}}
```shell
./pactus-wallet tx bond --pub <PUBLIC_KEY> <FROM> <TO> <AMOUNT>
```
  {{< /tab >}}

   {{< tab >}}
```shell
pactus-wallet.exe tx bond --pub <PUBLIC_KEY> <FROM> <TO> <AMOUNT>
```
  {{< /tab >}}
{{< /tabs >}}

Replace `<PUBLIC_KEY>` with the validator's public key,
which is the public key of the `<TO>` address.

### Sending Unbond Transaction

To create, sign, and broadcast a
[Unbond transaction](/docs/concepts/transaction/unbond/), use the following command:

{{< tabs items="Linux-mac,windows" >}}

  {{< tab >}}

```shell
./pactus-wallet tx unbond <ADDRESS>
```
  {{< /tab >}}

   {{< tab >}}

```shell
pactus-wallet.exe tx unbond <ADDRESS>
```
  {{< /tab >}}
{{< /tabs >}}

In this command, `<ADDRESS>` is the address of the validator that you want to unbond.

### Sending Withdraw Transaction

To create, sign, and broadcast a
[Withdraw transaction](/docs/concepts/transaction/withdraw/), use the following command:

{{< tabs items="Linux-mac,windows" >}}

  {{< tab >}}
```shell
./pactus-wallet tx withdraw <FROM> <TO> <AMOUNT>
```
  {{< /tab >}}

   {{< tab >}}
```shell
pactus-wallet.exe tx withdraw <FROM> <TO> <AMOUNT>
```
  {{< /tab >}}
{{< /tabs >}}
