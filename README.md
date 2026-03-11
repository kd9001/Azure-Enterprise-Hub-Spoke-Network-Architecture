# Azure-Enterprise-Hub-Spoke-Network-Architecture

## Overview
This project demonstrates a Hub-Spoke network architecture in Microsoft Azure following enterprise best practices.

## Architecture

Hub VNet
- Shared services
- Network routing

Spoke VNets
- Application workloads
- Subnet isolation

## Components

Hub
- VNet
- Shared subnet

Spokes
- Web subnet
- App subnet
- Virtual machines

## Networking

- VNet Peering
- Network Security Groups
- Segmented subnets

## Technologies Used

- Azure Virtual Network
- VNet Peering

##########################################################################################################

Architecture:


                     Internet
                        │
                        ▼
                  Azure Firewall
                        │
                        ▼
                     Hub VNet
                  10.0.0.0/16
        ┌──────────────┼──────────────┐
        │              │              │
   Bastion        VPN Gateway      Peering
        │              │              │
        ▼              ▼              ▼
     Spoke-App1                    Spoke-App2
     10.1.0.0/16                   10.2.0.0/16
        │                              │
  ┌─────┼─────┐                  ┌─────┼─────┐
  ▼     ▼     ▼                  ▼     ▼     ▼
 Web   App    DB                Web   App    DB

      
 We will create 3 RGs:
RG-Hub-Network
RG-Spoke-App1
RG-Spoke-App2





✅ This project will demonstrate:

Hub-Spoke architecture

Azure Firewall

Bastion

VPN Gateway

VNet Peering

Subnet segmentation

Enterprise networking


#################################################################################################

# Azure Hub & Spoke Network Project

## Overview
This project demonstrates a **Hub & Spoke network architecture** in Microsoft Azure, following enterprise best practices.  
It includes:

- **Hub VNet**: Centralized network, firewall, Bastion, and VPN Gateway
- **Spoke VNets**: Isolated application networks
- **Subnets**: Web, App, and DB tiers per spoke
- **VNet Peering**: Hub-to-Spoke routing
- **Network Security Groups**: Controlled inbound/outbound traffic
- **Azure Firewall**: Central security inspection
- **Azure Bastion**: Secure VM access

---

## Architecture Diagram

![Architecture Diagram](architecture/architecture-diagram.png)

**Description:**

- **Hub VNet**: 10.0.0.0/16, containing Firewall, Bastion, Gateway, and Shared Services subnets
- **Spoke-App1 VNet**: 10.1.0.0/16, subnets for Web, App, and DB
- **Spoke-App2 VNet**: 10.2.0.0/16, subnets for Web, App, and DB
- Traffic flows from Internet → Firewall → Hub → Spoke Web → App → DB
- Spoke-to-Spoke communication occurs through the Hub

---

## Components

| Component | Purpose |
|-----------|---------|
| Hub VNet | Central network, routing, security |
| Azure Firewall | Inspect and control traffic |
| Azure Bastion | Secure VM management (no public IP needed) |
| VPN Gateway | Simulated hybrid connectivity |
| Spoke VNets | Application networks |
| Subnets | Web / App / DB tiers |
| NSG | Control traffic per subnet |
| B1s VMs | Test web and app tier |

---

## Deployment Steps

1. Create Resource Groups
   - RG-Hub-Network
   - RG-Spoke-App1
   - RG-Spoke-App2
2. Create Hub VNet and subnets:
   - AzureFirewallSubnet, AzureBastionSubnet, GatewaySubnet, SharedServicesSubnet
3. Create Spoke VNets and subnets
4. Configure VNet peering (Hub ↔ Spokes)
5. Deploy Azure Firewall in hub
6. Deploy Bastion in hub
7. Deploy VPN Gateway in hub
8. Deploy small Linux VMs in web subnets
9. Configure NSGs for Web and App subnets
10. Test connectivity: Web → App → DB, Spoke-to-Spoke

---

## Cost Estimation

For **2 hours of deployment** (Azure Firewall + VPN Gateway + Bastion + 2 B1s VMs):

| Resource | Approx Cost |
|----------|-------------|
| Azure Firewall | $2.50 |
| VPN Gateway | $0.50 |
| Bastion | $0.40 |
| 2 VMs | $0.05 |
| **Total** | **≈ $3–4** |

> **Tip:** Delete all resources immediately after testing to avoid charges.

---

## Learning Outcomes

- Hub & Spoke network design in Azure
- Subnet tiering (Web/App/DB)
- Centralized security with Firewall and Bastion
- VNet peering and routing
- Cost-effective deployment strategy
- Infrastructure documentation using GitHub

---

## Screenshots

Include screenshots from Azure portal:

- Firewall and Bastion setup
- Spoke VNet subnets
- VMs running in web subnets



##################################################################################

| VNet       | Address Space | Subnets             | Subnet CIDR |
| ---------- | ------------- | ------------------- | ----------- |
| Hub        | 10.0.0.0/16   | AzureFirewallSubnet | 10.0.1.0/24 |
|            |               | AzureBastionSubnet  | 10.0.2.0/24 |
|            |               | GatewaySubnet       | 10.0.3.0/24 |
|            |               | SharedServices      | 10.0.4.0/24 |
| Spoke-App1 | 10.1.0.0/16   | web-subnet          | 10.1.1.0/24 |
|            |               | app-subnet          | 10.1.2.0/24 |
|            |               | db-subnet           | 10.1.3.0/24 |
| Spoke-App2 | 10.2.0.0/16   | web-subnet          | 10.2.1.0/24 |
|            |               | app-subnet          | 10.2.2.0/24 |
|            |               | db-subnet           | 10.2.3.0/24 |













- Network Security Groups
- Linux Virtual Machines
