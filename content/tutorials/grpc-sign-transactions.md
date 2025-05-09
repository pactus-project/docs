---
title: How to Sign Transactions Using gRPC?
weight: 5
---

## Preface

The Pactus Blockchain provides a gRPC interface that allows users to interact with the blockchain and native wallet.
This is ideal for merchants and users who want to create, sign, and broadcast transactions using their local node.
This tutorial will guide you step-by-step on how to use gRPC to sign transactions.

## Setup node

### Initialize the node

To follow along with this tutorial, you'll first need to set up and run a localnet blockchain, which is suitable for testing:

```bash
./pactus-daemon init \
  --localnet \
  --working-dir ./pactus-localnet \
  --password "super-secret-password" \
  --val-num 7 \
  --restore "fish cool avoid history kitten quick olive purchase blossom grocery cool treat"
```

This command initializes a Pactus blockchain as a localnet.
The purpose of this network is for testing.
The above command actually restores a node from the given mnemonic.
This helps you create the same wallet for this tutorial.
The first two addresses in this wallet are:

```text
tpc1zhv2hq30rnu9lkjusgwqk4f5qfdr72sd2mndnn6
tpc1zsrvuvn0j80vc3we5q44apjrv8j7ta5807z7xc7
```

We are going to transfer 1 PAC from the first account to the second one.

### Run the Node

Now you can run the node simply with this command:

```bash
./pactus-daemon start \
  --working-dir ./pactus-localnet \
  --password "super-secret-password"
```

By running the node, you will see that it starts creating blocks, and
therefore the reward account address will be rewarded locally.
We can use this balance for testing purposes.

### Interact with the Node

Open another terminal and run the following command:

```bash
./pactus-shell --server-addr localhost:50052 \
  blockchain get-blockchain-info
```

It should print information about the localnet blockchain.
The [Pactus Shell](https://docs.pactus.org/tutorials/pactus-shell/)
application uses gRPC to interact with the blockchain.
In this tutorial, we use Pactus Shell to interact with the blockchain.
You can either use
[JSON-RPC](https://docs.pactus.org/api/json-rpc/)
or make direct
[gRPC](https://docs.pactus.org/api/grpc/) API calls to interact with the node.
They are more or less similar and all interact with the node using gRPC endpoints.

## Signing Transactions

### Create the Raw Transaction

To sign a transaction, we first need to create a raw transaction and then sign it.
We can use the `get_raw_transfer_transaction` method to create a raw transfer transaction.
Similar methods can be used to create raw bond, unbond, and withdraw transactions.

```bash
./pactus-shell --server-addr localhost:50052 \
  transaction get-raw-transfer-transaction \
    --sender tpc1zhv2hq30rnu9lkjusgwqk4f5qfdr72sd2mndnn6 \
    --receiver tpc1zsrvuvn0j80vc3we5q44apjrv8j7ta5807z7xc7 \
    --amount 1
```

The sender account is the first reward address in the wallet, therefore it should have some coins in its account.

### Sign the Raw Transaction

Now you can sign this raw transaction. To sign a transaction,
first, we need to load the "default_wallet" wallet:

```bash
./pactus-shell --server-addr localhost:50052 \
  wallet load-wallet --wallet-name "default_wallet"
```

Now that the "default_wallet" is loaded, we can proceed to sign the raw transaction:

```bash
./pactus-shell --server-addr localhost:50052 \
  wallet sign-raw-transaction \
    --wallet-name "default_wallet" \
    --password "super-secret-password" \
    --raw-transaction "..."
```

Transaction successfully signed.

## Broadcast the Signed Transaction

Now you can broadcast the signed transaction:

```bash
./pactus-shell --server-addr localhost:50052 \
  transaction broadcast-transaction \
    --signed-raw-transaction "..."
```

Transaction successfully broadcasted.

## Production Security Considerations

In this tutorial, we utilized a localnet version of Pactus.
For production purposes, you'll need to set up the node for the Mainnet and synchronize it with the network.
Additionally, in production, the wallet service is disabled by default.
You can enable the wallet service in the configuration file.

When signing transactions in production, you need to prioritize the security of the wallet.
Make sure you have set a strong password for the native wallet.
Ensure that it is called on localhost for safety.
You can make the gRPC communication more secure in some ways.
For instance, [set a password](/tutorials/grpc-basic-auth/) for the gRPC service,
and [secure connections](/tutorials/secure-connections).
