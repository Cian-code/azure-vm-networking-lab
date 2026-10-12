# Azure Portal Screenshot Gallery

This gallery provides visual evidence for the [Azure VM & Networking Lab](../../). Each screenshot is paired with a short explanation of what was configured or inspected and why it matters.

## 01 — Azure resource inventory

![Azure Portal All resources view](01-resource-group.png)

**What this shows**

The Azure Portal's **All resources** view lists the resources used in the lab, including:

- `AZ900-VM01` — the Ubuntu virtual machine.
- `AZ900-VNet` — the virtual network.
- The VM's network security group and network interface.
- The managed OS disk, public IP resource, and SSH key resource.
- A Network Watcher resource in a separate resource group.

**What I did**

I deployed an Ubuntu VM in Azure and inspected the related resources Azure uses to provide compute, storage, and network connectivity. This view helped me see that a VM is supported by several distinct Azure resources rather than being a single standalone object.

**AZ-900 concepts demonstrated:** Azure resources, resource groups, virtual machines, networking resources, and managed disks.

## 02 — Virtual network address space

![AZ900-VNet address space](02-address-space.png)

**What this shows**

The address-space settings for `AZ900-VNet` in the Azure Portal. The configured address space is `10.0.0.0/16`, covering `10.0.0.0` through `10.0.255.255` (65,536 addresses in the range).

**What I did and learned**

I inspected the virtual network's address space and connected it to the subnet created for the VM. The VNet address space is the larger private address range; the subnet (`10.0.1.0/24`) is a smaller range within it. The VM's private IP, `10.0.1.4`, belongs to that subnet.

**AZ-900 concepts demonstrated:** Azure Virtual Network, CIDR notation, IP address ranges, subnets, and private IP addressing.

## Security and privacy

The screenshots are intended to show the Azure configuration without publishing the VM's public IP value or any credentials. Never upload the SSH private key, passwords, tokens, or other secrets. Review future screenshots for account details and subscription or tenant identifiers before adding them here.
