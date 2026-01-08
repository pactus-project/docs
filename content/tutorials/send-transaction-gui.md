---
title: Send Transactions in Graphic Mode
weight: 1
---

## Preface

The Pactus Blockchain offers a Graphical User Interface (GUI) that comes with a built-in wallet to create,
sign and broadcast transactions.
This tutorial aims to guide you step-by-step on how to use the GUI application to send transactions to the Pactus blockchain.
Whether you are a beginner or an advanced user, this tutorial is suitable for you.

## Prerequisites

Before we begin, you'll need to run the Pactus GUI application and ensure that it is synced with the network.
You can find detailed instructions on how to do this in the following [tutorial](/get-started/pactus-gui/).

## Sending a Transfer Transaction

To send a [transfer transaction](/protocol/transaction/transfer/), click on the "Transaction" menu and
select "Transfer".
A new window will appear where you can select the
[account](/protocol/blockchain/account/) address from which you wish to send the "transfer" transaction,
as well as the recipient's account address and the amount you wish to send.

After reviewing the transaction details and ensuring that they are correct,
click on the "Send" button to sign and broadcast the transaction to the Pactus blockchain.

![Transfer Transaction Dialog](/images/transfer-transaction-dialog.png)

Some exchanges and third-party services require a memo/tag to credit deposits correctly.
If the recipient provides a memo, include it to ensure the transaction is attributed properly.

## Sending a Bond Transaction

To send a [bond transaction](/protocol/transaction/bond/), click on the "Transaction" menu
and select "Bond".
A new window will appear where you can select the account address from which you wish to send the "bond" transaction,
as well as the recipient's [validator](/protocol/blockchain/validator/) address and
the amount you wish to stake.

![Bond Transaction Dialog](/images/bond-transaction-dialog.png)

If a validator does not yet exist, the public key of the validator should be set.
For an existing validator, a public key is not required.
Also, note that if the public key is not set, the system tries to search for it inside the wallet.
Therefore, if you want to stake on your own validators, you don't need to set the public key here.

## Unbond

To send a [unbond transaction](/protocol/transaction/unbond/), click on the "Transaction" menu
and select "Unbond".
A new window will appear where you can select the validator address from which you wish to "unbond".

![Unbond Transaction Dialog](/images/unbond-transaction-dialog.png)

## Withdraw

To send a [withdraw transaction](/protocol/transaction/withdraw/), click on the "Transaction" menu
and select "Withdraw".
A new window will appear where you can select the validator address from which you wish to withdraw their stake,
as well as the recipient's account address and the amount you wish to withdraw.

![Withdraw Transaction Dialog](/images/withdraw-transaction-dialog.png)
