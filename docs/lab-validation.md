# Lab validation log

The following commands were run inside the Ubuntu VM during the lab.

## Hostname

```bash
hostname
```

Observed output: `AZ900-VM01`.

## Interface addressing

```bash
ip address
```

The `eth0` interface was up and displayed `10.0.1.4/24`.

## Routing table

```bash
ip route
```

The table included:

- A directly connected route for `10.0.1.0/24` through `eth0`.
- A default route via `10.0.1.1`.
- A route to the Azure platform DNS address `168.63.129.16` via the Azure virtual network path.

## Outbound IP connectivity

```bash
ping -c 4 8.8.8.8
```

Observed result: 4 packets received, with 0% packet loss during the test.

## DNS resolution and connectivity

```bash
ping -c 4 google.com
nslookup google.com
resolvectl status
```

Observed results:

- `google.com` resolved to an IPv4 address and all four ping requests received replies during the test.
- `nslookup` displayed `127.0.0.53`, Ubuntu's local DNS stub resolver, and returned IPv4 and IPv6 records.
- `resolvectl status` listed `168.63.129.16` as the DNS server for `eth0`.

The public DNS answer is not recorded because DNS responses can change over time.

## Troubleshooting note

A ping to `10.0.1.1` received no ICMP replies, even though the routing table listed it as the default next hop. Outbound connectivity tests succeeded. An unsuccessful ping to a gateway address alone does not establish that the route is broken; results need to be checked together.
