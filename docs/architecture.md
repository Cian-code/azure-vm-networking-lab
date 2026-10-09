# Lab architecture

This diagram shows the major resources and logical associations used in the lab. The VM's public IP value and all credentials are intentionally omitted.

```mermaid
flowchart TB
  subgraph SUB[Azure subscription]
    subgraph RG[Resource group: AZ900-Lab]
      VM[AZ900-VM01<br/>Ubuntu Server 24.04 LTS]
      NIC[Network interface]
      DISK[Managed OS disk<br/>Standard SSD]
      PIP[Public IP resource<br/>Value omitted]
      VNET[AZ900-VNet<br/>10.0.0.0/16]
      SUBNET[AZ900-Subnet<br/>10.0.1.0/24]
      VM --> NIC
      VM --> DISK
      NIC --> SUBNET
      NIC --> PIP
      VNET --> SUBNET
    end
  end
  LAPTOP[Windows laptop / PowerShell]
  LAPTOP -->|SSH over TCP 22<br/>key-based authentication| PIP
```

## Addressing

- VNet address space: `10.0.0.0/16`
- Subnet range: `10.0.1.0/24`
- Private IP observed on the VM: `10.0.1.4`

The actual public IP, subscription IDs, and private SSH key are deliberately not documented.
