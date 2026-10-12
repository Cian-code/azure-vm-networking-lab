# Lab architecture

The diagram below shows the main Azure resources and their relationships. The actual public IP value and all credentials are omitted.

```mermaid
flowchart TB
  subgraph SUB["Azure subscription"]
    subgraph RG["Resource group: AZ900-Lab"]
      VNET["AZ900-VNet<br/>10.0.0.0/16"] --> SUBNET["AZ900-Subnet<br/>10.0.1.0/24"]
      VM["AZ900-VM01<br/>Ubuntu Server 24.04 LTS"] --> NIC["Network interface"]
      VM --> DISK["Managed OS disk<br/>Standard SSD"]
      NIC --> SUBNET
      NIC --> PIP["Public IP resource"]
      NSG["Network security group"] -. "network access rules" .-> NIC
    end
  end
  LAPTOP["Windows laptop / PowerShell"] -->|"SSH over TCP 22<br/>SSH key authentication"| PIP
```

## Addressing

- VNet address space: `10.0.0.0/16`
- Subnet address range: `10.0.1.0/24`
- Private IP observed inside the VM: `10.0.1.4`

The subnet is a smaller address range within the VNet's address space. The VM's network interface connects it to the subnet.

This diagram represents the lab configuration at a conceptual level; it does not expose the public IP value or identify any physical Azure infrastructure.
