---
title: How to interact with the Pactus JSON-RPC
weight: 5
---

## Intro

In this tutorial we are going to explain how you can call a Pactus node JSON-RPC API and get info from it using curl.
We go trough both APIs with parameters and without parameters. This document is also helpful if you wan't to interact with
JSON-RPC APIs of Pactus in your code.

## Pre-requirements

Before get started make sure you have these tools ready:

1. You must have [curl](https://curl.se/) installed on your machine properly.
2. You need a Pactus node API endpoint with JSON-RPC service enabled.

For the Pactus API you can whether use a public endpoint or run a local node for testing.

I'm going to use a local node on my machine to call JSON-RPC API. Here is my local node config:

```toml
[grpc]
  enable = true
  enable_wallet = true
  listen = "[::]:50052"
  basic_auth = ""

  [grpc.gateway]
    enable = true
    listen = "[::]:8080"
    enable_cors = false

[jsonrpc]
  enable = true
  listen = "127.0.0.1:8545"

[http]
  enable = false
  listen = "[::]:0"

[nanomsg]
  enable = false
  listen = "tcp://[::]:40799"
```

## Calling node info API

To call node info API, first of all we find our method name on JSON-RPC [documents](../api/json-rpc.md).

Then we put `pactus.network.get_node_info` in following request as our method name:

```json
{
    "jsonrpc": "2.0",
    "id": 1,
    "method": "pactus.network.get_node_info", // method name from documents.
    "params": {} // based on document this method don't accept params so we keep it empty.
}
```

> Note: make sure you add params field always even if there is no params needed and make sure you defined params using
curly braces not braces.

Then we put our JSON request as our curl command data:

```bash
curl --location 'http://localhost:8545/' \  # make sure you replace localhost:8545 with your own host and port if it's different.
--header 'Content-Type: application/json' \
--data ' {
    "jsonrpc": "2.0",
    "id": 1,
    "method": "pactus.network.get_node_info",
    "params": {}
  }'
```

After calling the method we will get the following result:

```json
{
   "jsonrpc":"2.0",
   "id":1,
   "result":{
      "moniker":"localnet-1",
      "agent":"node=daemon/node-version=1.5.0-beta/protocol-version=1/os=linux/arch=amd64",
      "peer_id":"002408011220bc6927cc1ed45c76bfeb39c5e6954364ae3b6c21fffeb2d623e531d9220fd7aa",
      "started_at":1723027485,
      "reachability":"Unknown",
      "services":3,
      "services_names":"FULL | PRUNED",
      "local_addrs":[
         "/ip4/127.0.0.1/tcp/36353",
         "/ip4/192.168.1.81/tcp/36353",
         "/ip6/::1/tcp/35885"
      ],
      "protocols":[
         "/ipfs/ping/1.0.0",
         "/ipfs/id/1.0.0",
         "/ipfs/id/push/1.0.0",
         "/pactus-localnet/stream/v1",
         "/meshsub/1.1.0",
         "/meshsub/1.0.0",
         "/floodsub/1.0.0"
      ],
      "connection_info":{
         
      }
   }
}
```

## Calling get account API

Based on the Pactus JSON-RPC [documents](../api/json-rpc.md) this method name is `pactus.blockchain.get_account`
and it accepts a parameter called `address` which is string.

We are going to get the Pactus fouditon account address details (`pc1z2r0fmu8sg2ffa0tgrr08gnefcxl2kq7wvquf8z`).

Here is our request:

```json
{
    "jsonrpc": "2.0",
    "id": 1,
    "method": "pactus.blockchain.get_account",
    "params": {
        "address" : "pc1z2r0fmu8sg2ffa0tgrr08gnefcxl2kq7wvquf8z"
    }
}
```

Then we put our request in our curl call:

```bash
curl --location 'http://localhost:8545/' \
--header 'Content-Type: application/json' \
--data ' {
    "jsonrpc": "2.0",
    "id": 1,
    "method": "pactus.blockchain.get_account",
    "params": {
        "address" : "pc1z2r0fmu8sg2ffa0tgrr08gnefcxl2kq7wvquf8z"
    }
  }'
```

We will get our result like this:

```json
{
   "jsonrpc":"2.0",
   "id":1,
   "result":{
      "account":{
         "hash":"a38c19e7c16e7920dd869181ec8ef377415c6e195c37cd09cb21114079e1d754",
         "data":"0100000000001d68c1d71d00",
         "number":1,
         "balance":8400000000000000,
         "address":"pc1z2r0fmu8sg2ffa0tgrr08gnefcxl2kq7wvquf8z"
      }
   }
}
```
