---
title: How to secure gRPC using basic authentication?
weight: 3
---

## Preface

The Pactus Blockchain offers a gRPC interface, enabling users to interact with both the blockchain
and its native wallet. To enhance the security of gRPC APIs, we have implemented a Basic Authentication
mechanism. This approach aims to provide a straightforward yet effective means for authenticating clients accessing the APIs.

**Note:** This mechanism secures gRPC, gRPC gateway, and HTTP communications.

## Generate Basic Auth

To enable basic authentication, you need to generate basic authentication credentials using an online
tool or a predefined utility.

Example Format:

```shell
username: foo
password: bar

result: foo:$2a$10$nl6VKEzSENIK5dmzoADgKeTFtCusQxeVCZiXkRzzbyfG.bLpHtrda
```

### Generate by using htpasswd tool

1. Install the `htpasswd` tool from [Apache](https://httpd.apache.org/docs/2.4/programs/htpasswd.html).
2. Use the `htpasswd` command-line tool to generate a bcrypt-hashed password. Here's the general syntax:

```shell
htpasswd -bnBC 10 <username> <password>
```

- `-b`: Use the command line to provide the password.
- `-n`: Output the hashed password to the console rather than updating a file.
- `-B`: Force the use of the bcrypt encryption algorithm.
- `-C cost`: Set the cost factor for the bcrypt algorithm. Higher values result in slower hashing but are more secure.
- `username`: The username for which you are generating the password.
- `password`: The password you wish to hash.

Example:

```shell
htpasswd -bnBC 10 user pass
```

This process results in a bcrypt-hashed password that can be used for basic authentication.

### Generate With Online tool

To generate basic authentication credentials, you can use the following form to create a hashed credential.

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

1. Open the `config.toml` file in your Pactus directory.

- Windows:`C:\Users\{user}\pactus`
- Linux and Mac: `/home/{user}/pactus`

2. Insert the generated user with the hashed password into the `basic_auth_credential` field in the config file.

```toml
[grpc]
enable = true
enable_wallet = false
listen = "127.0.0.1:50051"
basic_auth_credential = "foo:$2a$10$nl6VKEzSENIK5dmzoADgKeTFtCusQxeVCZiXkRzzbyfG.bLpHtrda"
```

3. Restart or run the node to apply this configuration.