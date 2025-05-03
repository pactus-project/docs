---
title: How to Secure Connections?
weight: 7
---

## Preface

As the Pactus blockchain grows, there is an increasing need for individuals and merchants to
communicate and interact with Pactus nodes.
Pactus offers several communication protocols, including
[gRPC](../api/grpc.md), [JSON-RPC](../api/json-rpc.md), and [HTTP](../api/http.md) APIs.
These protocols are part of the Pactus software, and users have control over enabling or disabling them.

In this tutorial, we will explore how to secure communication with Pactus nodes.
## Overview of Secure Communication Setup

You can configure the Pactus node to enable any of the communication protocols you may need. By default, only the gRPC protocol is enabled and accessible locally. Let's take a look at the default [Pactus Configuration](../get-started/configuration.md):

```toml
[grpc]
  enable = true
  listen = '127.0.0.1:50051'

  [grpc.gateway]
    enable = false
    listen = '127.0.0.1:8080'
    origins = []

[jsonrpc]
  enable = false
  listen = '127.0.0.1:8545'
  origins = []
```

> Note: The `grpc.gateway` enables a RESTful HTTP/JSON interface that maps to the same gRPC services.

The `enable` field determines whether the communication protocol is active.
The `listen` field defines the address where the protocol is accessible, in the format `<ADDRESS>:<PORT>`.
The port specifies which TCP port the protocol should use.
It’s important to choose a free port that isn’t already in use by another application.
The address is typically an IP address. Special addresses like `127.0.0.1` or `localhost`
are only accessible from within the local machine and are **not publicly accessible**.
We’ll explain the `origins` parameter later in this document.

![Pactus Localhost Connection](/images/secure-connections/pactus-connection-localhost.png)

You can change the address to make it publicly accessible—**which is not recommended**—for example: `0.0.0.0:50051`.
The address `0.0.0.0` tells the operating system to expose the port to all available network interfaces,
making the gRPC protocol accessible over the public IP of your server.
This allows anyone on the internet to potentially connect to your node.

![Pactus Insecure Connection](/images/secure-connections/pactus-connection-insecure.png)

To enable a secure communication protocol—or to upgrade HTTP to HTTPS—you need to register a domain name.
You cannot enable HTTPS for a plain IP address alone, because IP addresses can change frequently.
[TLS](https://en.wikipedia.org/wiki/Transport_Layer_Security)—the protocol that powers HTTPS—
**relies on domain names** to validate security certificates issued by trusted
[Certificate Authorities](https://en.wikipedia.org/wiki/Certificate_authority) (CAs).
These certificates are tied to specific domain names, not to IP addresses.
Therefore, a stable domain name is required to properly configure and maintain a secure connection.

There are many [domain name providers](https://www.google.com/search?q=Domain+Name+Provider) where you can purchase a domain.
Once you've registered a domain, you need to connect it to your server by configuring an `A Record` in your domain's DNS settings.
An `A Record` maps your domain name to the IPv4 address of your server, allowing visitors to reach your server using the domain.

To verify that the `A Record` is correctly set, you can use the
[dig](https://www.geeksforgeeks.org/dig-command-in-linux-with-examples/) command:

```bash
dig pactus.org +short
# Use your domain name here instead of pactus.org
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

This tutorial assumes you're running Pactus on a Linux machine,
and it covers various distributions.

### Install Nginx

Installing Nginx is straightforward:

{{< os_tabs items="debian,redhat,arch" >}}
  {{< os_tab >}}

```shell
sudo apt update
sudo apt install nginx
```

  {{< /os_tab >}}
  {{< os_tab >}}

```shell
sudo dnf install nginx
```

  {{< /os_tab >}}
    {{< os_tab >}}

```shell
sudo pacman -S nginx
```

  {{< /os_tab >}}
{{< /os_tabs >}}


After installation, you can start and enable Nginx service with:

```bash
sudo systemctl enable nginx
sudo systemctl start nginx
```

## Obtaining SSL Certificates with Certbot

Now that we have set up the reverse proxy, it’s time to obtain an SSL certificate to enable HTTPS.
We will use [Certbot](https://certbot.eff.org/), a free and widely used tool for automating the process of obtaining and renewing SSL certificates from [Let’s Encrypt](https://letsencrypt.org/).

### Installing Certbot

The installation process for Certbot is well-documented on its official website.
You can follow the specific instructions for your Linux distribution here:
[Certbot Installation Guide](https://certbot.eff.org/instructions).

### Obtaining the SSL Certificate

Once Certbot is installed, you can use it to obtain the SSL certificate.
Run the following command to obtain the certificate for your domain:

```bash
sudo certbot --nginx -d your-domain.com
```

Here’s what this command does:
- `--nginx`: Tells Certbot to automatically configure Nginx with the obtained SSL certificate.
- `-d your-domain.com`: Specifies the domain name you are obtaining the SSL certificate for.

If the domain is properly configured and pointing to your server, Certbot will:
1. Verify your domain ownership.
2. Obtain the SSL certificate from Let’s Encrypt.
3. Automatically configure Nginx to use HTTPS with the new certificate.

Now, you should be able to access your node securely via `https://your-domain.com`.
Try opening it in your browser to confirm that the secure connection is working.

### Configure Nginx

By default, Nginx is configured to load all `.conf` files in `/etc/nginx/conf.d/`.
Therefore, you can create a new configuration file for your Pactus setup there.
Using the [Nano text editor](https://www.geeksforgeeks.org/nano-text-editor-in-linux/), create the file `pactus.conf`:

```bash
sudo nano /etc/nginx/conf.d/pactus.conf
```

Paste the following content into the file:

```nginx {linenos=table,linenostart=1,hl_lines=[3,6,7]}
server {
    listen 443 ssl http2;
    server_name your-domain.com;

    # SSL configuration (only used if certs exist)
    ssl_certificate     /etc/letsencrypt/live/your-domain.com/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/your-domain.com/privkey.pem;
    include /etc/letsencrypt/options-ssl-nginx.conf;
    ssl_dhparam /etc/letsencrypt/ssl-dhparams.pem;

    # gRPC service
    location /grpc {
        grpc_pass grpc://127.0.0.1:50051/;
        grpc_set_header Host $host;
        grpc_set_header X-Real-IP $remote_addr;
        grpc_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    }

    # JSON-RPC
    location /jsonrpc {
        proxy_pass http://127.0.0.1:8545/;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }

    # gRPC Gateway (REST)
    location /grpc-gateway {
        proxy_pass http://127.0.0.1:8080/;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```

Make sure to replace `your-domain.com` with your actual domain name in lines 4, 7, and 8.

This configuration sets up Nginx as a reverse proxy[^1] for three endpoints:

- `/grpc` forwards requests to the gRPC server[^2] running on port `50051` on localhost.
- `/jsonrpc` forwards requests to the JSON-RPC server running on port `8545` on localhost.
- `/grpc-gateway` forwards requests to the RESTful gRPC Gateway server running on port `8080` on localhost.

It also includes the necessary SSL settings to enable HTTPS, which will be activated in the next step.



## References

[^1]: Learn more about the Nginx proxy module [here](https://nginx.org/en/docs/http/ngx_http_proxy_module.html).
[^2]: Nginx has native support for gRPC. Read more about it [here](https://blog.nginx.org/blog/nginx-1-13-10-grpc).


