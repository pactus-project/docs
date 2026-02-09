---
title: Connect GUI to Remote Node
weight: 8
---

Since Pactus version 1.12.0, users can connect to a remote node using the Pactus GUI. This enables them to easily monitor their node on any VPS from their personal computer. Managing your nodes, sending transactions, and monitoring validators can all be done through the GUI application.

In this document, we explain the ways you can connect to your node through the Pactus GUI.

## Bare Connection

To connect to your node, the [gRPC](https://grpc.io/docs/what-is-grpc/) service of your remote node must be enabled. The gRPC connection is unencrypted by default, so the connection between the GUI and your node is bare and unencrypted.

Here is an example of how you can connect to your node:

{{< os_tabs items="unix,windows" >}}
  {{< os_tab >}}

```shell
./pactus-gui -grpc-addr http://testnet1.pactus.org:50052 -grpc-insecure
```

  {{< /os_tab >}}
  {{< os_tab >}}

```shell
pactus-gui.exe -grpc-addr http://testnet1.pactus.org:50052 -grpc-insecure
```

  {{< /os_tab >}}
{{< /os_tabs >}}

You can use an IP address for the connection, such as `157.180.70.236:50052`. The `-grpc-insecure` flag indicates that the connection is not secure and not encrypted. We do not recommend enabling the wallet service in this mode, as all credentials and information you send or receive may be observed by a man-in-the-middle attacker.

## Secure Connection

One simple way to secure the gRPC connection is to wrap it over the `https` protocol. This is known as [gRPC-Web](https://grpc.io/docs/platforms/web/).

You can follow the [Secure Connections](./secure-connections.md) tutorial to set up your server to wrap the gRPC connection over the `https` protocol. We have explained how to secure the connection there. This approach requires a domain name and NGINX installed on your server.

Once the gRPC-Web setup is complete, you can connect to your node in a secure and encrypted way, as shown below:

{{< os_tabs items="unix,windows" >}}
  {{< os_tab >}}

```shell
./pactus-gui -grpc-addr https://testnet1.pactus.org/grpc-web
```

  {{< /os_tab >}}
  {{< os_tab >}}

```shell
pactus-gui.exe -grpc-addr https://testnet1.pactus.org/grpc-web
```

  {{< /os_tab >}}
{{< /os_tabs >}}

In this case, your connection from your computer to your node is fully encrypted and secure against man-in-the-middle attacks.

## Enabling Wallet Service

By default, the wallet service on your node is disabled. You can enable it in the config file; however, if your connection is insecure, we do not recommend it. If you do enable it, make sure you set a strong password for your wallet.

## FAQ

### I got a `server: 403 (Forbidden)` error

If you set up your domain using Cloudflare, this is most likely because the Cloudflare gRPC service is disabled. You can check their [documentation](https://developers.cloudflare.com/network/grpc-connections/#enable-grpc) to enable the gRPC service.
