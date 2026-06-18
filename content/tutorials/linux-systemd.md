---
title: Run Pactus as a Systemd Service
weight: 11
---

[Systemd](https://en.wikipedia.org/wiki/Systemd) is a system and service manager for Linux that
helps manage how programs start up, run, and shut down.
It also handles system processes, logging, and basic service monitoring.

## Prerequisites

Before setting up Pactus to run with systemd, ensure you have the following:

- Download the latest version of Pactus CLI for your Linux system from [here](https://pactus.org/download/#cli).
- This guide assumes that `systemd` is installed and running on your Linux distribution.
  Most modern distributions use `systemd` by default.

## Creating a systemd Service

After initializing your Pactus node with `pactus-daemon init`, you can set up
a systemd service to run it in the background.

1. **Create a Service File**: Open a terminal and
   create a new service file in the `/etc/systemd/system/` directory with superuser permissions:

   ```shell
   sudo nano /etc/systemd/system/pactus.service
   ```

2. **Add the Following Content** to the service file, replacing `<USER_NAME>` with your actual Linux username:

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

3. **Reload Systemd Configuration**: After creating or modifying the service file,
   reload the systemd to recognize the new service:

   ```shell
   sudo systemctl daemon-reload
   ```

4. **Start and Enable the Service**: Start the service immediately and enable it to start on boot:

   ```shell
   sudo systemctl start pactus
   sudo systemctl enable pactus
   ```

5. **Check Service Status**: Check the status of your service to ensure it is running correctly:

   ```shell
   sudo systemctl status pactus
   ```

## Checking Logs

If the service fails to start or behaves unexpectedly, check the logs using `journalctl`:

```shell
sudo journalctl -u pactus.service
```

This command will show you the log entries related to your service, helping you diagnose issues.
