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


#######################################################################################


🔹 Complete Deployment Order for Hub & Spoke Azure Project
________________________________________
Step 0 — Plan Your IPs
VNet	Address Space	Subnets	Subnet CIDR
Hub	10.0.0.0/16	AzureFirewallSubnet	10.0.1.0/24
		AzureBastionSubnet	10.0.2.0/24
		GatewaySubnet	10.0.3.0/24
		SharedServices	10.0.4.0/24
Spoke-App1	10.1.0.0/16	web-subnet	10.1.1.0/24
		app-subnet	10.1.2.0/24
		db-subnet	10.1.3.0/24
Spoke-App2	10.2.0.0/16	web-subnet	10.2.1.0/24
		app-subnet	10.2.2.0/24
		db-subnet	10.2.3.0/24
________________________________________
Step 1 — Create Resource Groups (RGs)
RG-Hub-Network
RG-Spoke-App1
RG-Spoke-App2
•	Hub RG: Hub VNet + Firewall + Bastion + VPN Gateway
•	Spoke RGs: VNets + VMs + Subnets
________________________________________
Step 2 — Create Hub VNet and Subnets
•	VNet Name: vnet-hub, Address: 10.0.0.0/16
•	Subnets:
AzureFirewallSubnet 10.0.1.0/24
AzureBastionSubnet  10.0.2.0/24
GatewaySubnet       10.0.3.0/24
SharedServices      10.0.4.0/24
Important: Azure requires exact names for Firewall, Bastion, and Gateway subnets.
________________________________________
Step 3 — Create Spoke VNets and Subnets
Spoke-App1
•	VNet Name: vnet-spoke-app1, Address: 10.1.0.0/16
•	Subnets:
web-subnet 10.1.1.0/24
app-subnet 10.1.2.0/24
db-subnet  10.1.3.0/24
Spoke-App2
•	VNet Name: vnet-spoke-app2, Address: 10.2.0.0/16
•	Subnets:
web-subnet 10.2.1.0/24
app-subnet 10.2.2.0/24
db-subnet  10.2.3.0/24
________________________________________
Step 4 — Configure VNet Peering
Create Hub ↔ Spokes:
1.	Hub ↔ Spoke-App1
2.	Hub ↔ Spoke-App2
Settings:
•	Hub side:
o	Allow forwarded traffic ✅
o	Allow gateway transit ✅
•	Spoke side:
o	Use remote gateway ✅
This enables spoke-to-spoke communication via Hub.
________________________________________
5️⃣ Create Network Security Groups (Important)
Create 3 NSGs per spoke.
NSG-Web
Allow HTTP (80) from Internet
Allow SSH (22) from your IP
Deny all other inbound
NSG-App
Allow traffic from web-subnet
Deny internet access
NSG-DB
Allow traffic only from app-subnet
Deny all other traffic
________________________________________
6️⃣ Attach NSGs to Subnets
Attach like this:
Spoke-App1
web-subnet → NSG-Web
app-subnet → NSG-App
db-subnet  → NSG-DB
Spoke-App2
web-subnet → NSG-Web
app-subnet → NSG-App
db-subnet  → NSG-DB
Now traffic is controlled at subnet level.
________________________________________
7️⃣ Configure VNet Peering
Create:
vnet-hub ↔ vnet-spoke-app1
vnet-hub ↔ vnet-spoke-app2
Settings:
Hub side:
Allow forwarded traffic ✓
Allow gateway transit ✓
Spoke side:
Use remote gateway ✓
________________________________________
8️⃣ Deploy Azure Firewall
Location:
AzureFirewallSubnet
Purpose:
•	Inspect traffic
•	Centralized security
•	Route spoke traffic
________________________________________
9️⃣ Deploy Azure Bastion
Location:
AzureBastionSubnet
Purpose:
•	Secure SSH/RDP
•	No public IP on VMs
________________________________________
🔟 Deploy VPN Gateway
Location:
GatewaySubnet
Purpose:
•	Hybrid connectivity
•	Simulates enterprise architecture
________________________________________
1️⃣1️⃣ Deploy VMs
Deploy small B1s Linux VMs.
Example:
Spoke-App1
VM-Web-App1 → web-subnet
Spoke-App2
VM-Web-App2 → web-subnet
Optional:
•	App VM
•	DB VM
But for cost control, deploy only web VMs.
________________________________________
1️⃣2️⃣ Updated Traffic Flow (With NSGs)
User accessing application
User
 │
 ▼
Internet
 │
 ▼
Azure Firewall (Hub)
 │
 ▼
Hub VNet
 │
 ▼
VNet Peering
 │
 ▼
Spoke Web Subnet (NSG-Web)
 │
 ▼
App Subnet (NSG-App)
 │
 ▼
DB Subnet (NSG-DB)
________________________________________
1️⃣3️⃣ Internal Application Flow
Inside Spoke-App1:
Web VM
 │
 ▼
App Subnet
 │
 ▼
DB Subnet
Allowed because:
•	NSG-Web allows inbound HTTP
•	NSG-App allows traffic from Web
•	NSG-DB allows traffic from App
________________________________________
1️⃣4️⃣ Spoke-to-Spoke Communication
Example:
VM-App1
 │
 ▼
Hub Firewall
 │
 ▼
VM-App2
Traffic is inspected by hub security layer.
________________________________________
1️⃣5️⃣ Full Traffic Flow Diagram
                 Internet
                     │
                     ▼
               Azure Firewall
                     │
                     ▼
                  Hub VNet
                     │
          ┌──────────┴──────────┐
          ▼                     ▼
      Spoke-App1            Spoke-App2
         │                       │
   ┌─────┼─────┐           ┌─────┼─────┐
   ▼     ▼     ▼           ▼     ▼     ▼
 Web   App    DB         Web   App    DB
(NSG) (NSG) (NSG)       (NSG) (NSG) (NSG)
________________________________________
1️⃣6️⃣ Cost for 2 Hours
Resource	Cost
Azure Firewall	~$2.50
VPN Gateway	~$0.50
Bastion	~$0.40
2 B1s VMs	~$0.05
Total:
💰 ~$3–4








