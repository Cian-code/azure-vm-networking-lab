# Azure VM & Networking Lab

Hands-on Microsoft Azure lab documenting the deployment of an Ubuntu virtual machine and practical checks of its network configuration.

## Project overview

The goal of this project was to build a small Azure environment through the Azure Portal, connect to a Linux VM remotely, and use basic Linux networking tools to understand IP addressing, routing, and DNS resolution. This is an introductory learning lab, not a production architecture.

## Environment

| Component | Configuration |
|---|---|
| Resource group | `AZ900-Lab` |
| Region | South Africa North |
| Availability zone | Zone 1 |
| Virtual network | `AZ900-VNet` (`10.0.0.0/16`) |
| Subnet | `AZ900-Subnet` (`10.0.1.0/24`) |
| VM | `AZ900-VM01` |
| OS | Ubuntu Server 24.04 LTS |
| Size | Standard B2ats_v2 (2 vCPUs, 1 GiB RAM as displayed in the Portal) |
| OS disk | Managed Standard SSD |
| Private IP observed inside the VM | `10.0.1.4` |
| Remote administration | SSH using public-key authentication |

Public IP addresses, subscription identifiers, and private-key material are intentionally excluded.

## Screenshot evidence

The [Azure Portal screenshot gallery](docs/screenshots/README.md) documents the resource inventory and VNet address space, with captions explaining what each screenshot demonstrates.

## Work completed

- Created the resource group, virtual network, and subnet in the Azure Portal.
- Deployed an Ubuntu Linux VM in South Africa North, Zone 1.
- Inspected the VM size, OS disk, network interface, private IP, and public connectivity configuration.
- Connected from Windows PowerShell using SSH and a private key stored locally.
- Used Linux commands to inspect hostname, interface addressing, and routing.
- Tested outbound IP connectivity and DNS-based connectivity.
- Identified the configured Azure-provided DNS resolver and observed IPv4 and IPv6 DNS answers.
- Stopped/deallocated the VM when not actively using the lab.

## Practical validation

| Command | Purpose | Observed result |
|---|---|---|
| `hostname` | Identify the VM | Returned `AZ900-VM01` |
| `ip address` | Inspect interfaces and IP configuration | `eth0` showed `10.0.1.4/24` |
| `ip route` | Inspect connected and default routes | Included `10.0.1.0/24` via `eth0` and default route via `10.0.1.1` |
| `ping -c 4 8.8.8.8` | Test outbound IP connectivity | 4 replies received; 0% packet loss during the test |
| `ping -c 4 google.com` | Test DNS resolution and connectivity | Name resolved and 4 replies were received during the test |
| `nslookup google.com` | Inspect DNS lookup results | Returned IPv4 and IPv6 address records |
| `resolvectl status` | Inspect resolver configuration | Listed `168.63.129.16` for `eth0`; `nslookup` displayed the local stub resolver at `127.0.0.53` |

### Troubleshooting observation

A ping to `10.0.1.1` received no ICMP replies, while outbound connectivity to `8.8.8.8` succeeded. A gateway/next-hop address not responding to ping does not, by itself, prove that routing or outbound connectivity is broken.

## AZ-900 concepts practised

- Azure resources, resource groups, and subscriptions
- Regions and availability zones
- Virtual machines and VM sizing
- Virtual networks, subnets, network interfaces, and IP addressing
- Public versus private IP addresses
- SSH remote access and key-based authentication
- Basic routing and DNS resolution

## Security notes

- SSH over TCP port 22 was enabled for this learning lab.
- For production workloads, restrict SSH source addresses and consider controlled access options such as Azure Bastion or private connectivity.
- The VM's public IP, subscription identifiers, and SSH private key are not included.
- `.gitignore` can help exclude local secrets, but it is not a substitute for keeping credentials out of a repository.

## Scope and limitations

This repository documents the VM and networking tasks actually deployed and tested. App Service, Azure Container Instances, VM Scale Sets, Availability Sets, Azure Virtual Desktop, and VNet peering were explored as AZ-900 concepts, but were not deployed as part of this lab.

## Possible next steps

- Add sanitized Azure Portal screenshots of the resource group, VNet/subnet, and VM overview.
- Continue with VNet peering, VPN Gateway, ExpressRoute, and public/private endpoints.
- Add storage, identity, governance, and monitoring exercises as separate documented labs.

Created as a personal hands-on learning project while studying Microsoft Azure fundamentals.