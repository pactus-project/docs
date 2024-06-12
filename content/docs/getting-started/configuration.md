---
title: Pactus Node Configuration
weight: 6
---

This configuration list specifies
[configurations](https://github.com/pactus-project/pactus/blob/main/config/example_config.toml) for running a Pactus node.

## Node

| Key              | Type            | Description                                                                |
| ---------------- | --------------- | -------------------------------------------------------------------------- |
| reward_addresses | array of string | specifies the addresses for collecting rewards, if empty, reward addresses |
will be obtained from the wallet, if it has only one address, it is used for all validators,
otherwise, the number of reward addresses should be the same as the number of validators. |

## Store

| Key  | Type   | Description                                                                        |
| ---- | ------ | ---------------------------------------------------------------------------------- |
| path | string | specifies the directory where blockchain data will be stored, default is `"data"`. |

## Network

| Key                   | Type            | Description                                                                                                                                                                                                                            |
| --------------------- | --------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| network_key           | string          | specifies the private key filename to use for node authentication and encryption in the p2p protocol, default is `"network_key"`.                                                                                                      |
| public_addr           | string          | public_addr is the the address that is public and accessible to other nodes.                                                                                                                                                           |
| listen_addrs          | array of string | specifies the addresses and ports where the node will listen for incoming connections from other nodes.                                                                                                                                |
| bootstrap_addrs       | array of string | bootstrap_addrs is a list of peer addresses needed for peer discovery, these addresses are used by the Pactus node to discover and connect to other peers on the network                                                               |
| max_connections       | intger          | max_connections is the maximum number of connections that the Pactus node maintains, default is `64`                                                                                                                                   |
| enable_udp            | boolean         | indicates whether the UDP transport protocol should be enabled or not, enabling UDP can improve the network connectivity of the node, but it might also lead to many packet losses, default is `false`                                 |
| enable_nat_service    | boolean         | provides a service to other peer for determining their reachability status, default is `false`                                                                                                                                         |
| enable_upnp           | boolean         | will attempt to open a port in your network's firewall using UPnP, default is `false`                                                                                                                                                  |
| enable_relay          | boolean         | indicates whether relay service should be enabled or not, relay service is a transport protocol that routes traffic between two peers over a third-party “relay” peer, default is `true`                                               |
| enable_relay_service  | boolean         | indicates whether relay service should be enabled or not, relay service is a transport protocol that enables peers to discover each other on the peer-to-peer network, default is `false`                                              |
| enable_mdns           | boolean         | indicates whether MDNS should be enabled or not, MDNS is a protocol to discover local peers quickly and efficiently, default is `false`                                                                                                |
| enable_metrics        | boolean         | provides the network metrics for the Prometheus software, default is `false`                                                                                                                                                           |
| force_private_network | boolean         | forces the connection to nodes within a private network, a private network is a computer network that uses private addresses, read more about private networks here: https://en.wikipedia.org/wiki/Private_network, default is `false` |

## Sync

| Key                    | Type    | Description                                                                                                                                                                                                                                                                           |
| ---------------------- | ------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| moniker                | string  | moniker is a custom human-readable name for this node.                                                                                                                                                                                                                                |
| session_timeout        | string  | session_timeout is a timeout for a download session to remain open, when a block download request is sent, this timer starts. If there is no activity from the target Node, the session will be closed after the timeout and try to get the block from another Node, default is `10s` |
| node_network           | boolean | indicates whether the node is capable of serving the complete blockchain, default is `true`                                                                                                                                                                                           |
| [sync.firewall].enable | boolean | indicates whether the firewall should be enabled or not, default is `false`                                                                                                                                                                                                           |

## Tx Pool

| Key       | Type   | Description                                                                                                                        |
| --------- | ------ | ---------------------------------------------------------------------------------------------------------------------------------- |
| max_size  | intger | indicates the maximum number of unconfirmed transactions inside the pool, default is `1000`.                                       |
| min_value | float  | indicates the minimum value of a transaction in PAC to enter into the pool, this prevents spamming transactions, default is `0.1`. |

## Logger

| Key                   | Type            | Description                                                                                                       |
| --------------------- | --------------- | ----------------------------------------------------------------------------------------------------------------- |
| colorful              | boolean         | indicates whether log can be colorful or not, default is `true`.                                                  |
| max_backups           | intger          | max_backups is the maximum number of old log files to retain, default is `0`.                                     |
| rotate_log_after_days | intger          | rotate_log_after_days is the maximum number of days to retain old log files, default is `0`.                      |
| compress              | boolean         | determines if the rotated log files should be compressed, default is `true`.                                      |
| targets               | array of string | etermines where the logs will be shown, saved, or sent, default is `["console", "file"]`.                         |
| [logger.levels]       | section         | contains the level of logger per module, available log levels are: "trace", "debug", "info", "warn", and "error". |

## GRPC

| Key           | Type    | Description                                                                                                                                           |
| ------------- | ------- | ----------------------------------------------------------------------------------------------------------------------------------------------------- |
| enable        | boolean | indicates whether gRPC service should be enabled or not, default is `true`.                                                                           |
| enable_wallet | boolean | indicates whether Wallet service should be enabled or not, default is `false`.                                                                        |
| listen        | string  | listen is the address to listen for incoming connections for gRPC server, default for mainnet `127.0.0.1:50051` and for testnet is `127.0.0.1:50052`. |
| basic_auth    | string  | is the Basic Auth credential used to enhance gRPC security, [for more details](../../tutorials/grpc-basic-auth)                                       |

## GRPC Gateway

| Key         | Type    | Description                                                                                                     |
| ----------- | ------- | --------------------------------------------------------------------------------------------------------------- |
| enable      | boolean | indicates whether gRPCGateway service should be enabled or not, default is `false`.                             |
| listen      | string  | listen is the address to listen for incoming connections for gRPCGateway server.                                |
| enable_cors | string  | indicates whether Cross-Origin Request Sharing (CORS), protection should be enabled or not, default is `false`. |

## Json RPC

| Key    | Type    | Description                                                                      |
| ------ | ------- | -------------------------------------------------------------------------------- |
| enable | boolean | indicates whether JSON-RPC service should be enabled or not, default is `false`. |
| listen | string  | listen is the address to listen for incoming connections for JSON-RPC server.    |

## Http

| Key    | Type    | Description                                                                  |
| ------ | ------- | ---------------------------------------------------------------------------- |
| enable | boolean | indicates whether HTTP service should be enabled or not, default is `false`. |
| listen | string  | is the address to listen for incoming connections for HTTP server.           |

## Nanomessage

| Key    | Type    | Description                                                                     |
| ------ | ------- | ------------------------------------------------------------------------------- |
| enable | boolean | indicates whether nanomsg service should be enabled or not, default is `false`. |
| listen | string  | is the address to listen for incoming connections for nanomsg server.           |
