---
title: Reduce Network Usage
weight: 9
---

## Preface

Pactus is designed for low traffic usage.
However, some users still face bandwidth limitations imposed by their Internet Service Providers (ISPs).
This guide will explore effective ways to reduce network usage for a Pactus node.

## Reducing the number of connections

By default, Pactus attempts to maintain 64 open connections with other nodes,
with 1/4 of these as outbound connections and the remaining as inbound connections.
To reduce network usage, you can decrease this maximum number of connections.
However, it's important to remember that more connections with
peers usually enable the node to function more effectively and securely.
The `max_connections` setting in the [config](/get-started/configuration/) file
can be adjusted to manage the maximum number of connections.

## Disabling Relay

A relay connection is a type of connection that can be established between two peers,
usually behind a NAT, by a third-party peer known as a relay.
This is especially helpful when users run Pactus on a private network like a home network.
However, the relay connection is not as stable as a direct connection.
Disabling the relay connection may reduce network usage.
If you have a reliable and public IP address, you can disable the relay connection.
The relay connection is enabled by default. To disable the relay connection,
set `enable_relay` to `false` inside the [config](/get-started/configuration/) file.
