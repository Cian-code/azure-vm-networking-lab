# Lab validation notes

These notes summarize commands run during the lab. They are for learning and do not represent a complete production troubleshooting procedure.

## Identify the VM

Command: `hostname`

Observed output: `AZ900-VM01`.

## Inspect the Linux interface

Command: `ip address`

Observation: interface `eth0` was up and displayed IPv4 address `10.0.1.4/24`.

## Inspect routing

Command: `ip route`

- `10.0.1.0/24` was listed as directly connected through `eth0`.
- The default route was via `10.0.1.1`.
- A route involving `168.63.129.16` appeared via the Azure virtual network path.

## Test outbound connectivity

Command: `ping -c 4 8.8.8.8`

Observed result: 4 packets received and 0% packet loss during the test.

## Test DNS resolution and connectivity

Command: `ping -c 4 google.com`

Observed result: `google.com` resolved to an IPv4 address and all 4 ping requests received replies during the test. The resolved public address is omitted because DNS answers can change.

## Inspect DNS

Commands: `nslookup google.com` and `resolvectl status`

- `nslookup` displayed `127.0.0.53`, Ubuntu's local DNS stub resolver.
- `resolvectl status` listed `168.63.129.16` as the configured/current DNS server for `eth0`.
- The lookup returned both IPv4 and IPv6 records.

## Troubleshooting lesson

A ping to `10.0.1.1` did not receive ICMP replies, despite the route table listing it as the default gateway. Outbound connectivity tests succeeded. An unsuccessful ping to a gateway address alone does not prove routing is broken; use multiple checks and interpret results in context.
