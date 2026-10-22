# cloud-engineering-Project-3-VMs-and-Network-on-Azure
# Project 3: Enterprise Hybrid-OS Network Architecture & RBAC Security Profiles on Azure

## 📌 Project Overview
Designed and deployed a highly isolated, mixed-operating system enterprise infrastructure environment on Microsoft Azure. Configured dedicated network spaces, strict network interface security group boundaries, managed data storage expansions, and validated enterprise compliance structures by enforcing least-privilege Role-Based Access Controls (RBAC) via Microsoft Entra ID.

## 🏗️ Architecture Implementations

* **Isolated Cloud Networking (VNet):** Configured a primary virtual network (`vnet-core`) utilizing a `10.10.0.0/16` routing boundary. Segregated the space into two isolated subnets to enforce architectural boundaries:
  * `subnet-linux` (`10.10.1.0/24`)
  * `subnet-windows` (`10.10.2.0/24`)
* **Granular Network Firewalls (NSG):** Provisioned separate Network Security Groups (NSGs) for individual subnets. Implemented strict inbound connection profiles utilizing explicit IP whitelisting to block public ingress vectors:
  * `nsg-linux`: Restricts inbound access solely to **SSH Port 22** from the administrator's authorized public IP address.
  * `nsg-windows`: Restricts inbound access solely to **RDP Port 3389** from the administrator's authorized public IP address.
* **Mixed-OS Architecture & Data Provisioning:** 
  * Provisioned an **Ubuntu Server 24.04 LTS** instance running inside the dedicated Linux subnet.
  * Provisioned a **Windows Server 2025 Datacenter** instance running inside the Windows subnet, executing a storage extension via an attached **32 GiB Premium Managed Data Disk**.
* **Identity Governance & Restrictive RBAC:** Provisioned a custom directory test identity (`test-reader`) within **Microsoft Entra ID**. Enforced security principles by assigning a granular, read-only **Reader Role** restricted to the scope of the parent resource group.

## ⚡ Compliance & Security Audit Verification
Validated least-privilege enforcement parameters by launching an active audit session under the `test-reader` credentials. Attempts to invoke infrastructure mutations—specifically executing an instance termination or stop action—were immediately intercepted and rejected by the Azure Resource Manager evaluation layer.

## 📁 Repository Artifacts
* `README.md` - Technical documentation and architecture layout.

## 📸 Architectural Infrastructure & Security Proofs
<img width="1440" height="859" alt="Screenshot (11)" src="https://github.com/user-attachments/assets/2589bfcd-b388-4311-bfe9-a72ebb1eb0e6" />
<img width="1440" height="860" alt="Screenshot (12)" src="https://github.com/user-attachments/assets/17ad8444-5f8d-4508-acbc-e5dccff083b6" />

### Microsoft Entra ID RBAC Authorization Denied Verification:
<img width="1440" height="900" alt="Screenshot (8)" src="https://github.com/user-attachments/assets/36f2e6de-aa36-4eee-92b6-d62e3029a524" />
