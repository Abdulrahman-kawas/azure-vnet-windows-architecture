# Azure VNet Multi-Tier Architecture & VM Connectivity

## 📝 Overview
This project demonstrates the design and deployment of a secure, multi-tier cloud network infrastructure on Microsoft Azure. It focuses on provisioning a Virtual Network (VNet) with isolated subnets and establishing internal routing and communication between two Windows Server Virtual Machines without exposing the backend to the public internet.

## 🏗️ Architecture & Environment Details
The infrastructure was deployed in the **Korea South** region within the `first-rg` resource group. 

### Network Configuration
* **Virtual Network (VNet):** `my-vnet`
* **Address Space:** `172.16.0.0/16`

### Subnets & Compute Resources
**1. Front-End Environment:**
* **Subnet Name:** `front-subnet` (`172.16.1.0/24`)
* **Virtual Machine:** `front-vm` (Windows Server 2025 Datacenter)
* **Public IP:** `20.214.58.152`
* **Private IP:** `172.16.1.4`

**2. Back-End Environment:**
* **Subnet Name:** `back-subnet` (`172.16.0.0/24`)
* **Virtual Machine:** `back-vm` (Windows Server 2025 Datacenter)
* **Private IP:** `172.16.0.4` (No Public IP attached for security)

## ⚙️ Deployment Steps
The following logical steps were executed to build this environment:
1. Provisioned the Virtual Network (`my-vnet`) and segmented it into `front-subnet` and `back-subnet`.
2. Deployed `front-vm` into the front-end subnet with public RDP access.
3. Deployed `back-vm` into the back-end subnet using only a private IP.
4. Established an external RDP session to the `front-vm`.
5. Initiated an internal RDP session from `front-vm` to `back-vm` across the VNet to validate private routing.

## 📸 Proof of Work

### 1. Virtual Machines Deployment
The images below show the running VMs and their assigned IP configurations in the Azure Portal.

**Front-End VM Details:**
![Front VM Details](frontend-Screenshot%202026-07-02%20135425.png)

**Back-End VM Details (Highlighting the Private IP):**
![Back VM Details](get-privet-ip-Screenshot%202026-07-02%20135750.png)

### 2. External Access Validation
Connecting to the `front-vm` securely via Native RDP using its Public IP.
![External RDP Connection](contact-VM-frontendScreenshot%202026-07-02%20135519.png)

### 3. Internal Connectivity Validation (The Ultimate Proof)
To prove that the Virtual Network correctly routes traffic between the subnets, an RDP connection was successfully established **from within** the `front-vm` directly to the `back-vm` using its private IP (`172.16.0.4`) and the local administrator account (`adminkawas`).

*(The screenshot below demonstrates the internal RDP prompt originating from the front-end VM)*
![Internal Connectivity Proof](remote-contactScreenshot%202026-07-02%20140224.png)

### 💡 Key Takeaway: VNet Default Routing
By deploying this architecture, we successfully demonstrated a core Azure networking concept: **Virtual Machines located in different subnets within the same Virtual Network (VNet) can communicate with each other by default.** 

Even though `front-vm` and `back-vm` are isolated in their own respective subnets (`front-subnet` and `back-subnet`), the overarching VNet automatically routes the internal traffic between them using their private IP addresses, ensuring seamless and secure backend communication.


## 🛠️ Skills Demonstrated
* Cloud Infrastructure Provisioning (Microsoft Azure)
* Azure Virtual Networks (VNets) & Subnetting
* Windows Server Cloud Administration
* Private Network Routing & Secure Remote Access (RDP)
