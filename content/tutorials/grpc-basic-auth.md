---
title: How to Secure gRPC Using Basic Authentication?
weight: 6
---

## Preface

The Pactus Blockchain offers a gRPC interface, enabling users to interact with the blockchain
and its native wallet. To enhance the security of gRPC APIs, we have implemented a Basic Authentication
mechanism based on [bcrypt](https://en.wikipedia.org/wiki/Bcrypt) password hashing.
This approach aims to provide a straightforward yet effective means for authenticating clients accessing the APIs.

**Note:** This mechanism secures gRPC, gRPC gateway, JSON-RPC, and HTTP communications.

## Basic Auth Format

Basic Authentication is a string of the form `username:password_hash`.
For example, if the username is "user" and the password is "pass", the Authorization header would be:

```text
user:$2a$10$nl6VKEzSENIK5dmzoADgKeTFtCusQxeVCZiXkRzzbyfG.bLpHtrda
```

## Generate Password Hash

You can generate a bcrypt-hashed password using the following methods:

### Using Apache htpasswd

The [Apache htpasswd](https://httpd.apache.org/docs/2.4/programs/htpasswd.html)
is a simple application for generating password hashes.
Here is the general syntax:

```shell
htpasswd -bnB <username> <password>
```

- `b`: Use batch mode to retrieve the password from the command line rather than prompting for it.
- `n`: Display the results on standard output.
- `B`: Force the use of the bcrypt algorithm.
- `username`: The username for which the password is being generated.
- `password`: The password to be hashed.

Example:

```shell
htpasswd -bnB user pass
```

This process results in a bcrypt-hashed password that can be used for basic authentication.

### Using Online tool

To generate basic authentication credentials, you can use this online tool here.
For additional security, you can save the web page locally and run it on an offline computer.

{{<basic-auth>}}

</br>
<form id="passwdForm">
  <label for="username">Username</label><br />
  <input type="text" id="username" name="username" /><br />
  <label for="password">Password</label><br />
  <input type="password" id="password" name="password" /><br /><br />
  <button type="button" class="custom-button" onclick="generateHtpasswd(event)">
    Generate
  </button>
  <br>
  <br>
  <p id="output"></p>
</form>

## Enable Basic Auth in the Config

To enable Basic Authentication in your Pactus Blockchain configuration, follow these steps:

1. Open the [configuration](https://docs.pactus.org/get-started/configuration/) file in your Pactus directory.
2. Insert the generated user with the hashed password into the `basic_auth` field in the `grpc` section:

```toml
[grpc]
enable = true
enable_wallet = false
listen = "127.0.0.1:50051"
basic_auth = "user:$2a$10$nl6VKEzSENIK5dmzoADgKeTFtCusQxeVCZiXkRzzbyfG.bLpHtrda"
```

3. Restart or run the node to apply this configuration.
