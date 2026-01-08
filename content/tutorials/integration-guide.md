---
title: Pactus Integration Guide
weight: 13
---

## Preface

This guide is intended for developers and infrastructure teams who want to connect
their applications directly to the Pactus network, including wallets, exchanges,
analytics platforms, staking services, and custom backend systems.

In particular, this document is especially useful for **exchange integrations**,
as Pactus allows exchanges to send transactions, monitor incoming transfers, and
track balances directly via a native Pactus node, without relying on any
third-party APIs or external indexing services.

## Run a Pactus Node

Running a Pactus node is simple and can be done in just a few steps. Pactus is
designed to be lightweight and easy to operate. You can set up and run a Pactus
node either as a [system service](/get-started/pactus-daemon/) or using
[Docker](/get-started/pactus-docker/) on your servers.

Although Pactus storage is optimized and running a full node is recommended, you
may run the node in [pruned mode](/tutorials/pruned-nodes/) if you have limited
storage. A pruned node does not retain the entire blockchain history; instead,
it keeps blocks and transactions only for a configured retention period. By
default, the retention period is set to 10 days, but you can increase it to
higher values (for example, 365 days) to retain transactions for a longer time.

## Node Endpoints

Pactus provides multiple endpoints, including [JSON-RPC](/api/json-rpc/),
[gRPC](/api/grpc/), and [HTTP](/api/http/).

The gRPC service is the primary gateway for interacting with a Pactus node and
should be enabled. For security reasons, we recommend not exposing these
endpoints publicly and restricting access to `localhost` or a private network.

You may use any of these endpoints depending on your integration requirements.

## Enable Wallet Service

Each Pactus node includes a secure, embedded wallet service for managing funds.
This service is disabled by default and can be enabled through the node
[config](/get-started/configuration/) file.

Exercise caution when enabling the wallet service and follow security best
practices at all times.

We strongly recommend setting a **strong password** for all wallets. Ideally,
wallet-related APIs should not be exposed publicly. If public access is
required, ensure all communications are properly secured by enabling
authentication and encryption. See
[gRPC Basic Authentication](https://docs.pactus.org/tutorials/grpc-basic-auth/)
[gRPC Basic Authentication](https://docs.pactus.org/tutorials/grpc-basic-auth/)
and
[Secure Connections](https://docs.pactus.org/tutorials/secure-connections/) for
detailed instructions on protecting Pactus endpoints and preventing
unauthorized access.

## Manage Wallets

By default, each Pactus node includes an integrated wallet named
`default_wallet`. However, you can create multiple wallets as needed. Each
wallet may serve a different purpose. For example, one wallet for receiving
funds and another for sending transactions.

You may also create a **neuter wallet**, which is a special wallet without
private keys. Neuter wallets cannot sign transactions but can generate and
manage addresses for receiving funds. This is useful for deposit tracking and
monitoring incoming transactions without exposing private keys.

Create and manage wallets according to your operational and security strategy.

## Send Transactions

Transactions are sent through the wallet service. To send a transaction, you
must first create a **raw (unsigned) transaction**, then sign it using a wallet,
and finally broadcast it to the network.

To create a raw transaction, use the
[Transaction](/api/grpc/#getrawtransfertransaction) service and provide the
required information, such as the sender and receiver addresses. This returns an
unsigned transaction payload.

You can then use the wallet service to
**[sign](/api/grpc/#signrawtransaction)** the transaction. The sender address
must belong to your wallet. The signed transaction can be broadcast to the
network using **[BroadcastTransaction](/api/grpc/#broadcasttransaction)**.

Once a transaction is committed and included in a block, it is finalized and
confirmed. You can retrieve the confirmed transaction details using the
**[GetTransaction](/api/grpc/#gettransaction)** API. If, for any reason, your
transaction is not included in any block, the `GetTransaction` API will return
an error, indicating that the transaction has not been finalized or confirmed.

## Check for Incoming Transactions

Each wallet scans and monitors every block for incoming transactions and stores
them in its database. You can query and list wallet transactions using the
[ListTransaction](/api/grpc/#listtransactions) API. Transactions can be filtered
by direction (incoming or outgoing) or by address. Pagination options such as
`count` and `skip` can be used to efficiently navigate large transaction
histories.
