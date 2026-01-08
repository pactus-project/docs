---
title: Secure Connections
weight: 7
---

## Preface

As the Pactus blockchain grows, the need for individuals and merchants to
communicate and interact with Pactus nodes is increasing.
Pactus provides several communication protocols,
including [gRPC](/api/grpc), [JSON-RPC](/api/json-rpc), and [HTTP](/api/http) APIs.
These protocols are built into the Pactus software, and users can choose to enable or disable them as needed.

In this tutorial, we will explain how to secure communication with Pactus nodes.

## Overview of Secure Communication Setup

You can configure the Pactus node to enable any of the communication protocols you need. By default,
only the gRPC protocol is enabled and accessible locally.
Here's the default [Pactus Configuration](/get-started/configuration):

```toml
[grpc]
  enable = true
  enable_wallet = false
  listen = '127.0.0.1:50051'
  basic_auth = ''

[jsonrpc]
  enable = false
  listen = '127.0.0.1:8545'
  origins = []

[http]
  enable = false
  listen = '127.0.0.1:8080'
  base_path = '/http'
  origins = []
```

The `enable` field determines whether the communication protocol is active.

The `listen` field defines the address where the protocol is accessible, in the format `<ADDRESS>:<PORT>`.
The port specifies which TCP port the protocol should use.
Choose a free port that isn't already in use by another application.
The address is typically an IP address.
Special addresses like `127.0.0.1` or `localhost` are only accessible locally and are **not publicly accessible**.

The `origins` field controls CORS (Cross-Origin Resource Sharing),
specifying which web domains can access the API (e.g., "wallet.pactus.org").
Use `*` to allow all domains (not recommended for production).

![Pactus Localhost Connection](/images/secure-connections/pactus-connection-localhost.png)

You can change the address to make it publicly accessible—**which is not recommended**—for example: `0.0.0.0:50051`.
The address `0.0.0.0` tells the operating system to expose the port to all available network interfaces,
making the protocol accessible over the public IP of your server.
This allows anyone on the internet to potentially connect to your node.

![Pactus Insecure Connection](/images/secure-connections/pactus-connection-insecure.png)

To enable a secure communication protocol—or to upgrade HTTP to HTTPS—you need to register a domain name.
You cannot enable HTTPS for a plain IP address, because the
[TLS](https://en.wikipedia.org/wiki/Transport_Layer_Security), the protocol that powers HTTPS,
**relies on domain names** to validate security certificates issued by trusted
[Certificate Authorities](https://en.wikipedia.org/wiki/Certificate_authority) (CAs).
These certificates are tied to specific domain names, not to IP addresses.
Therefore, a stable domain name is required to properly configure and maintain a secure connection.

There are many [domain name providers](https://www.google.com/search?q=Domain+Name+Provider) where you can purchase a domain.
Once you've registered a domain,
you need to connect it to your server by configuring an `A Record` in your domain's DNS settings.
An `A Record` maps your domain name to the IPv4 address of your server,
allowing visitors to reach your server using the domain.

Verify the `A Record` using the
[dig](https://www.geeksforgeeks.org/dig-command-in-linux-with-examples/) command:

```bash
dig pactus.org +short
# Replace pactus.org with your domain
```

If the configuration is correct, this will return the IP address associated with your domain.

Once your domain is correctly assigned to your server’s IP, we can begin securing the communication protocol.
To secure communication, we will use [Nginx](https://nginx.org/).
Nginx is a free, open-source, and secure web server that can act as a
[reverse proxy](https://en.wikipedia.org/wiki/Reverse_proxy).
A *reverse proxy* means that Nginx stands between external clients (users) and your internal services (like the Pactus node).
It accepts incoming requests on behalf of your server, handles the secure TLS/HTTPS connection,
and forwards the request to your Pactus node over the internal network.

![Pactus Secure Connection](/images/secure-connections/pactus-connection-secure.png)

This setup ensures that sensitive APIs are never directly exposed to the internet.
Only Nginx is exposed, and it acts as a security gateway.
Users communicate securely with Nginx, which handles encryption and certificate validation.
If the connection is valid, Nginx forwards the request to the Pactus node,
then sends the response back to the user over the secure channel.

## Setup Secure Communication

This tutorial assumes you're running Pactus on a Linux <i class="fa-brands fa-linux"></i> machine,
and it covers Debian <i class="fa-brands fa-debian"></i> or Ubuntu <i class="fa-brands fa-ubuntu"></i> distributions.
However, the steps are similar for other Linux distributions.

### Install Nginx

Installing Nginx is straightforward:

```bash
sudo apt update
sudo apt install nginx
```

After installation, you can start and enable Nginx service with:

```bash
sudo systemctl enable nginx
sudo systemctl start nginx
```

At this point if you visit your website with `http://your-domain.com`,
you should be able to see the Nginx Welcoming message:

![Nginx Welcoming message](/images/secure-connections/nginx-welcoming-screen.png)

## Obtaining SSL Certificates

Now that we have set up the reverse proxy, it’s time to obtain an SSL certificate to enable HTTPS.
We will use [Certbot](https://certbot.eff.org/),
a free and widely used tool for automating the process of obtaining and renewing SSL certificates from
[Let’s Encrypt](https://letsencrypt.org/).

The [Certbot Instructions](https://certbot.eff.org/instructions) is well-documented on its official website.
Choose Nginx as HTTP software and Linux (snap) as your system and continue the instructions.

If the domain is properly configured and pointing to your server, Certbot will:

1. Verify your domain ownership.
2. Obtain the SSL certificate from Let’s Encrypt.
3. Automatically configure Nginx to use HTTPS with the new certificate.

Now, you should be able to access your node securely via `https://your-domain.com`.
Try opening it in your browser to confirm that the secure connection is working.

## Configure Nginx

The Nginx configuration can be found at `/etc/nginx/sites-available/default`.
Before changing the config file, first let's make a backup of that.

```bash
sudo mv /etc/nginx/sites-available/default /etc/nginx/sites-available/default_bak
```

Now, using the [Nano text editor](https://www.geeksforgeeks.org/nano-text-editor-in-linux/),
let's create a new configuration file:

```bash
sudo nano /etc/nginx/sites-available/default
```

Paste the following content into the file:

```nginx{linenos=table,linenostart=1,hl_lines=[6,8,21,23,24]}
## HTTP Server Block
server {
    listen 80;
    listen [::]:80;

    server_name your-domain.com;

    if ($host = your-domain.com) {
        # Redirect HTTP to HTTPS
        return 301 https://$host$request_uri;
    }

    return 404;
}

## HTTPS Server Block
server {
    listen [::]:443 ssl ipv6only=on;
    listen 443 ssl http2; # http2 is required for grpc-web

    server_name your-domain.com;

    ssl_certificate     /etc/letsencrypt/live/your-domain.com/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/your-domain.com/privkey.pem;
    include             /etc/letsencrypt/options-ssl-nginx.conf;
    ssl_dhparam         /etc/letsencrypt/ssl-dhparams.pem;

    ####################################
    ## reverse proxy block for gRPC-Web
    location /grpc-web {
        # Enable CORS for gRPC-Web
        add_header 'Access-Control-Allow-Origin' '*';
        add_header 'Access-Control-Allow-Methods' 'GET, POST, OPTIONS';
        add_header 'Access-Control-Allow-Headers' 'Content-Type, Authorization, x-grpc-web, x-user-agent';

        if ($request_method = 'OPTIONS') {
            return 204;
        }

        rewrite ^/grpc-web/(.*) /$1 break; # remove /grpc-web prefix

        grpc_pass grpc://127.0.0.1:50051;
        grpc_set_header Content-Type application/grpc;
        grpc_set_header X-Forwarded-For $remote_addr;
    }

    ####################################
    ## reverse proxy block for JSON-RPC
    location /jsonrpc {
        proxy_pass http://127.0.0.1:8545/;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }

    ####################################
    ## reverse proxy block for HTTP-API
    location /http {
        proxy_pass http://127.0.0.1:8080/http;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```

Make sure to replace `your-domain.com` with your actual domain name in lines 6, 8, 21, 23, and 24.

This configuration sets up Nginx as a reverse proxy for three endpoints:

- `/grpc-web` forwards requests to the gRPC server running on port `50051` on localhost.
- `/jsonrpc` forwards requests to the JSON-RPC server running on port `8545` on localhost.
- `/http` forwards requests to the HTTP API server running on port `8080` on localhost.

### Verify and Restart Nginx

Before applying changes, always test your Nginx configuration:

```bash
sudo nginx -t
```

This command checks for syntax errors in your configuration files.
If you see "syntax is ok" and "test is successful", you can safely restart Nginx:

```bash
sudo systemctl restart nginx
```

### Testing Your Connection

We've built a simple testing tool at [https://ping.pactus.org](https://ping.pactus.org)
that you can use to verify your node's connectivity and HTTPS configuration.

## References

- Learn more about the Nginx proxy module [here](https://nginx.org/en/docs/http/ngx_http_proxy_module.html).
- Nginx has native support for gRPC. Read more about it [here](https://blog.nginx.org/blog/nginx-1-13-10-grpc).
