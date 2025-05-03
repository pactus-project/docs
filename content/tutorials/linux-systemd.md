---
title: How to Run Pactus with systemd on Linux?
weight: 10
---

## Preface

[Systemd](https://en.wikipedia.org/wiki/Systemd) is a system and service manager for Linux that
helps manage how programs start up, run, and shut down.
It also handles system processes, logging, and basic service monitoring.

## Prerequisites

Before setting up Pactus to run with systemd, ensure you have the following:

- Download the latest version of Pactus CLI for your Linux system from [here](https://pactus.org/download/#cli).
- This guide assumes that `systemd` is installed and running on your Linux distribution.
  Most modern distributions use `systemd` by default.

## Creating a systemd Service

To create a systemd service for Pactus, follow these steps:

1. **Initialize the Pactus Node**: Before running the service, initialize the Pactus node by this command:

  ```shell
  pactus-daemon init
  ```

2. **Create a Service File**: Open a terminal and
  create a new service file in the `/etc/systemd/system/` directory with superuser permissions:

  ```shell
  sudo nano /etc/systemd/system/pactus.service
  ```

3. **Add the Following Content** to the service file, replacing `<USER_NAME>` with your actual username:

  ```ini
  [Unit]
  Description=Pactus Daemon Service
  After=network.target

  [Service]
  Type=simple
  User=<USER_NAME>
  ExecStart=/home/<USER_NAME>/pactus-cli/pactus-daemon start -w /home/<USER_NAME>/pactus
  Restart=on-failure
  RestartSec=10

  [Install]
  WantedBy=multi-user.target
  ```

4. **Reload Systemd Configuration**: After creating or modifying the service file,
   reload the systemd to recognize the new service:

  ```shell
  sudo systemctl daemon-reload
  ```

5. **Start and Enable the Service**: Start the service immediately and enable it to start on boot:

  ```shell
  sudo systemctl start pactus
  sudo systemctl enable pactus
  ```

6. **Check Service Status**: Check the status of your service to ensure it is running correctly:

  ```shell
  sudo systemctl status pactus
  ```

## Managing the Service

Use these commands to manage the Pactus service with systemd:

- **Start the Service**:

  ```shell
  sudo systemctl start pactus
  ```

- **Stop the Service**:

  ```shell
  sudo systemctl stop pactus
  ```

- **Restart the Service**:

  ```shell
  sudo systemctl restart pactus
  ```

- **Enable the Service to Start on Boot**:

  ```shell
  sudo systemctl enable pactus
  ```

- **Disable the Service from Starting on Boot**:

  ```shell
  sudo systemctl disable pactus
  ```

## Checking Logs

If the service fails to start or behaves unexpectedly, check the logs using `journalctl`:

```shell
sudo journalctl -u pactus.service
```

This command will show you the log entries related to your service, helping you diagnose issues.
