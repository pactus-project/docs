---
title: Use Pactus Shell
weight: 3
---

Pactus Shell is a command-line tool designed for interacting with the Pactus blockchain.
This tool receives commands from the terminal and sends them to the node using gRPC.
The resulting response is then displayed in a structured [JSON](https://www.json.org) format.

You can execute `pactus-shell` with the `-h` flag to display available commands for communicating with your node.

{{< os_tabs items="unix,windows" >}}
  {{< os_tab >}}

```shell
./pactus-shell -h
```

  {{< /os_tab >}}
  {{< os_tab >}}

```shell
pactus-shell.exe -h
```

  {{< /os_tab >}}
{{< /os_tabs >}}

## Example

Suppose you want to get the latest blockchain information.
In that case, you can use the following command in the `pactus-shell`:

{{< os_tabs items="unix,windows" >}}
  {{< os_tab >}}

```shell
./pactus-shell blockchain get-blockchain-info
```

  {{< /os_tab >}}
  {{< os_tab >}}

```shell
pactus-shell.exe blockchain get-blockchain-info
```

  {{< /os_tab >}}
{{< /os_tabs >}}

## Server address

By default, the exposed port of the Pactus gRPC node is `50051`.
Therefore, when you use `pactus-shell`, it automatically attempts to connect to `localhost:50051`.
However, you can easily change the default address by using the `--server-addr` flag.
For instance, if you want to connect to a remote server, you can execute:

{{< os_tabs items="unix,windows" >}}
  {{< os_tab >}}

```shell
./pactus-shell blockchain get-blockchain-info --server-addr example.com:50051
```

  {{< /os_tab >}}
  {{< os_tab >}}

```shell
pactus-shell.exe blockchain get-blockchain-info --server-addr example.com:50051
```

  {{< /os_tab >}}
{{< /os_tabs >}}

## Security consideration

When connecting to a remote node, it's important to think about security.
You can make the gRPC communication more secure in some ways.
For instance, [set a password](/tutorials/grpc-basic-auth/) for the gRPC service,
and [secure connections](/tutorials/secure-connections).
