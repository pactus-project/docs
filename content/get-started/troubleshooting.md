---
title: Troubleshooting Pactus Node
weight: 5
---

Below, we have identified a series of issues that might interfere with the node's execution process.
By reviewing each of the following points, you can resolve network connectivity or other related problems.

## NTP (Network Time Protocol) is not enabled

If your system or server clock is more than 5 to 10 seconds ahead or behind,
it will cause interference with your node on the network and may also
reduce your `availability score`, preventing you from receiving rewards.

To check and enable NTP on your system:

### Windows

Open `cmd` as administrator and run `w32tm /query /status`. If disabled, use `w32tm /resync` to synchronize.

Alternatively, install the graphical SNTP client from
<a href="https://www.timesynctool.com/" rel="nofollow noindex noreferrer" target="_blank">timesynctool.com</a>.
For advanced configuration, refer to the
<a href="https://learn.microsoft.com/en-us/windows-server/networking/windows-time-service/windows-time-service-tools-and-settings?tabs=config"
rel="nofollow noindex noreferrer" target="_blank">Windows Time Service documentation</a>.

### Linux

Run `timedatectl status`. If NTP is inactive, enable it with `timedatectl set-ntp true`.

### macOS

Open Terminal and check with `sntp -s time.apple.com`.

## Port P2P is open in local machine or server

One of the most important factors that causes interference with the node's communication is the P2P input and
output ports not being open.
If you have a firewall, you should check this.

- Default Port for mainnet is: `21888`
- Default Port for testnet is: `21777`

You can check whether this port is open or closed using
<a href="https://portchecker.co/" rel="nofollow noindex noreferrer" target="_blank">portchecker</a>
or similar online tools.

![Open port in firewall](/images/open-port.png)

## Avoid Running Duplicated Nodes

Do not attempt to run node with same validators on different machines,
as this will reduce the `availability score` of your validators.
See
<a href="https://pactus.org/2024/12/04/the-risk-of-running-duplicated-nodes/"
rel="nofollow noindex noreferrer" target="_blank">The Risk of Running Duplicated Nodes</a>
for more details.

## Enable UDP in config

If your node encounters issues with synchronization in its default settings, you can use UDP.
Refer to the <a href="../configuration">configuration page</a> for details on enabling UDP and other network settings.
