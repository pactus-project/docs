---
title: How to run Pactus with systemd linux?
weight: 8
---

Systemd is a system and service manager for Linux operating systems.
It is designed to provide better efficiency, performance, and manageability over the traditional SysV init system.
systemd is a suite of basic building blocks for a Linux system that provides a system and service manager that
runs as PID 1 and starts the rest of the system.

## Prerequisites

- Download the latest version of Pactus CLI for your Linux system from [here](https://pactus.org/download/#cli).
- Systemd: This guide assumes that systemd is installed and running on your Linux distribution.
- Most modern Linux distributions use systemd by default.

## How to create systemd service?

First, create a systemd service file for `pactus-daemon` file. This file will tell systemd how to manage your service.

1. Open a terminal and create a new service file in the `/etc/systemd/system/` directory.
2. You will need superuser permissions to do this.

```shell
sudo nano /etc/systemd/system/pactus.service
```

2. Add the following content to the file, replacing `{user}` with your actual username:

```ini
[Unit]
Description=Pactus Daemon Service
After=network.target

[Service]
Type=simple
User={user}
ExecStart=/home/{user}/pactus-cli/pactus-daemon start -w /home/{user}/pactus
Restart=on-failure
RestartSec=10

[Install]
WantedBy=multi-user.target
```

{{< callout type="info" >}}
Before running the service, you need to initialize the Pactus service by using `pactus-daemon init`.
{{< /callout >}}

3. After creating or modifying the service file,
  you need to reload the systemd manager configuration to recognize the new service.

```shell
sudo systemctl daemon-reload
```

1. To start the service immediately and enable it to start on boot, use the following commands:

```shell
sudo systemctl start pactus
sudo systemctl enable pactus
```

5. You can check the status of your service to ensure it is running correctly:

```shell
sudo systemctl status pactus
```

```shell
● pactus.service - Pactus Daemon Service
     Loaded: loaded (/etc/systemd/system/pactus.service; disabled; preset: enabled)
     Active: active (running) since Sun 2024-05-26 11:12:54 +0330; 10s ago
   Main PID: 90107 (pactus-daemon)
      Tasks: 22 (limit: 40623)
     Memory: 27.2M (peak: 28.9M)
        CPU: 5.486s
     CGroup: /system.slice/pactus.service
             └─90107 home/{user}/pactus-cli/pactus-daemon start -w /home/{user}/pactus

May 26 11:13:05 15ALC6 pactus-daemon[90107]: 11:13:05 INF new block committed _state="{#1281 ⌘ 6E41D64CFE33 🕣 03.27.30}" block="{⌘ 6E41D64CFE33 👤 pc1p378jgjtl 💻 58CE193E0161 📨 1}" round>
May 26 11:13:05 15ALC6 pactus-daemon[90107]: 11:13:05 INF new block committed _state="{#1282 ⌘ 366B03DCF65A 🕣 03.27.40}" block="{⌘ 366B03DCF65A 👤 pc1plq8uyn6e 💻 F098577447DB 📨 1}" round>
May 26 11:13:05 15ALC6 pactus-daemon[90107]: 11:13:05 INF new block committed _state="{#1283 ⌘ D69C65555B92 🕣 03.27.50}" block="{⌘ D69C65555B92 👤 pc1pm93ykyvc 💻 CD768CBD0F2C 📨 1}" round>
May 26 11:13:05 15ALC6 pactus-daemon[90107]: 11:13:05 INF new block committed _state="{#1284 ⌘ D66E9A24F92A 🕣 03.28.00}" block="{⌘ D66E9A24F92A 👤 pc1pp3xtmjhz 💻 8ED750F438CA 📨 1}" round>
May 26 11:13:05 15ALC6 pactus-daemon[90107]: 11:13:05 INF new block committed _state="{#1285 ⌘ 8B60B8F624AD 🕣 03.28.10}" block="{⌘ 8B60B8F624AD 👤 pc1p378jgjtl 💻 964C484CC19D 📨 1}" round>
May 26 11:13:05 15ALC6 pactus-daemon[90107]: 11:13:05 INF new block committed _state="{#1286 ⌘ E0FA657D6E76 🕣 03.28.20}" block="{⌘ E0FA657D6E76 👤 pc1plq8uyn6e 💻 D9616D8C437E 📨 1}" round>
May 26 11:13:05 15ALC6 pactus-daemon[90107]: 11:13:05 INF new block committed _state="{#1287 ⌘ 077FD6637930 🕣 03.28.30}" block="{⌘ 077FD6637930 👤 pc1pm93ykyvc 💻 DA04DE4E9224 📨 1}" round>
May 26 11:13:05 15ALC6 pactus-daemon[90107]: 11:13:05 INF new block committed _state="{#1288 ⌘ 2954EAAFEB9F 🕣 03.28.40}" block="{⌘ 2954EAAFEB9F 👤 pc1pp3xtmjhz 💻 D1D2556F0BC1 📨 1}" round>
May 26 11:13:05 15ALC6 pactus-daemon[90107]: 11:13:05 INF new block committed _state="{#1289 ⌘ 4EF8FCF3141B 🕣 03.28.50}" block="{⌘ 4EF8FCF3141B 👤 pc1p378jgjtl 💻 FA9707153527 📨 1}" round>
May 26 11:13:05 15ALC6 pactus-daemon[90107]: 11:13:05 INF new block committed _state="{#1290 ⌘ 2F47F91619DE 🕣 03.29.00}" block="{⌘ 2F47F91619DE 👤 pc1plq8uyn6e 💻 B9924A951389 📨 1}" round>
May 26 11:13:05 15ALC6 pactus-daemon[90107]: 11:13:05 INF new block committed _state="{#1291 ⌘ 424D4CEB70AA 🕣 03.29.10}" block="{⌘ 424D4CEB70AA 👤 pc1pm93ykyvc 💻 AE210F198107 📨 1}" round>
lines 1-21/21 (END)
```

## Manage the Service

Here are some common commands to manage the service:

- Start the service:

```shell
sudo systemctl start pactus
```

- Stop the service:

```shell
sudo systemctl stop pactus
```

- Restart the service:

```shell
sudo systemctl restart pactus
```

- Enable the service to start on boot:

```shell
sudo systemctl enable pactus
```

- Disable the service from starting on boot:

```shell
sudo systemctl disable pactus
```

## Troubleshooting

If the service fails to start or behaves unexpectedly, you can check the logs using `journalctl`:

```shell
sudo journalctl -u pactus.service
```

This command will show you the log entries related to your service, which can help you diagnose issues.
