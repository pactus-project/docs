---
title: Troubleshooting Pactus Node
weight: 5
---

Below, we have identified a series of issues that might interfere with the node's execution process. By reviewing each of the following points, you can resolve network connectivity or other related problems.

## NTP (Network Time Protocol) is not enabled

Network Time Protocol (NTP) is an internet protocol used to synchronize with computer clock time sources in a network.

If your system or server clock is more than 5 to 10 seconds ahead or behind, it will cause interference with your node on the network and may also reduce your `availability score`, preventing you from receiving rewards.

Therefore, make sure to check that your system or server clock is fully synchronized and that NTP is enabled.

{{< tabs items="Windows,Linux-Mac" >}}

{{< tab >}}
1. Run `cmd` with run as administrator.
2. Check NTP is enable
```shell
w32tm /query /status
```

If this command result is `The following error occurred: The service has not been started. (0x80070426)`, follow step 3 for enable and sync ntp.

3. Unregister w32time with `w32tm /unregister`

```shell
W32Time successfully unregistered.
```
4. Then register w32time again `w32tm /register`

```shell
W32Time successfully registered.
```
5. Now start w32time service `net start w32time`

```shell
The Windows Time service is starting.
The Windows Time service was started successfully.
```
6. Check NTP status `w32tm /query /status`
```shell
Leap Indicator: 3(not synchronized)
Stratum: 0 (unspecified)
Precision: -23 (119.209ns per tick)
Root Delay: 0.0000000s
Root Dispersion: 0.0000000s
ReferenceId: 0x00000000 (unspecified)
Last Successful Sync Time: unspecified
Source: Local CMOS Clock
Poll Interval: 10 (1024s)
```
If `Leap Indicator` is not synchronized, please following step 7.

7. Set NTP pool `w32tm /config /manualpeerlist:pool.ntp.org /syncfromflags:manual /reliable:yes /update`
```shell
The command completed successfully.
```
8. Update configuration `w32tm /config /update`
```shell
The command completed successfully.
```
9. Sync system by command `w32tm /resync /rediscover`
```shell
Sending resync command to local computer
The command completed successfully.
```
10. Now local computer currently synced with ntp pool.
```shell
Leap Indicator: 0(no warning)
Stratum: 3 (secondary reference - syncd by (S)NTP)
Precision: -23 (119.209ns per tick)
Root Delay: 0.7217312s
Root Dispersion: 8.1410050s
ReferenceId: 0xBC7D4007 (source IP:  188.125.64.7)
Last Successful Sync Time: 5/27/2024 11:05:14 PM
Source: pool.ntp.org
Poll Interval: 10 (1024s)
```
{{< /tab >}}

{{< tab >}}
1. Run `terminal`.
2. Check NTP status by `timedatectl status`
```shell
               Local time: Tue 2024-05-28 07:19:21 BST
           Universal time: Tue 2024-05-28 06:19:21 UTC
                 RTC time: Tue 2024-05-28 06:19:21
                Time zone: Europe/London (BST, +0100)
System clock synchronized: yes
              NTP service: active
          RTC in local TZ: no
```

If `NTP service` is not active and `System clock synchronized` is no please following step 3.

3. Enable NTP using `ntpq`, `chrony` or `systemd-timesyncd`.

- <a href="https://timetoolsltd.com/ntp/how-to-install-and-configure-ntp-on-linux/" rel="nofollow noindex noreferrer" target="_blank">How to enable NTP service by ntpq</a>
- <a href="https://ubuntu.com/server/docs/how-to-serve-the-network-time-protocol-with-chrony" rel="nofollow noindex noreferrer" target="_blank">How to enable NTP service by chrony</a>
- <a href="https://groups.google.com/g/public-ntp-discuss/c/VhXAirp-28c" rel="nofollow noindex noreferrer" target="_blank">How to enable NTP service by systemd-timesyncd</a>

{{< /tab >}}

{{< /tabs >}}

## Port P2P is open in local machine or server

One of the most important factors that causes interference with the node's communication is the P2P input and output ports not being open. If you have a firewall, you should check this.

- Default Port for mainnet is: `21888`
- Default Port for testnet is: `21777`

You can check by <a href="https://portchecker.co/" rel="nofollow noindex noreferrer" target="_blank">online service</a> for this port is open or close.

![Open port in firewall](/images/open-port.jpg)

## Avoid running node with the same validators on different machines

Do not attempt to run node with same validators on different machines, as this will reduce the `availability score` of your validators.

## Using UDP instead relay for sync

If your node encounters issues with synchronization in its default settings, you can use UDP.

- Example network configuration:

```toml
[network]
  network_key = "network_key"
  public_addr = ""
  listen_addrs = []
  bootstrap_addrs = []
  max_connections = 128
  enable_udp = true
  enable_nat_service = false
  enable_upnp = false
  enable_relay = false
  enable_relay_service = false
  enable_mdns = false
  enable_metrics = false
  force_private_network = false
```
