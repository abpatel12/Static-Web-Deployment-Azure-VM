# Project 1: Multi-Site Hosting on Azure VM via IIS

This repository highlights the deployment of two distinct static HTML/CSS web applications hosted on a single Microsoft Azure Windows Server VM using **Internet Information Services (IIS)**. The sites are bound to different ports (`80` and `8080`) and are accessible both locally inside the virtual machine and publicly over the internet.

---

## 🌐 Project Architecture & Setup

- **Cloud Platform:** Microsoft Azure
- **Operating System:** Windows Server 2022
- **Web Server:** Internet Information Services (IIS)
- **Hosted Applications:**
  1. **Barista Cafe Template** (Bound to Port `80`)
  2. **Choco-Lux Template** (Bound to Port `8080`)

---

## 🛠️ Step-by-Step Implementation

### 1. Web Server (IIS) Installation
- Connected to the Azure VM via Remote Desktop Connection (RDP).
- Opened **Server Manager** and initialized the **Add Roles and Features Wizard**.
- Selected and installed the **Web Server (IIS)** role along with the **IIS Management Console**.

### 2. Website 1: Barista Cafe (Port 80)
- Placed the extraction files inside the default directory: `C:\inetpub\wwwroot`.
- **Verification:**
  - **Inside VM:** Accessible via local loopback / internal configuration.
  - **Outside VM:** Publicly accessible across the internet via the VM's public IP address over standard HTTP port `80`.

### 3. Website 2: Choco-Lux (Port 8080)
- Created a custom directory for the second site at `C:\inetpub\site2`.
- Opened **IIS Manager**, added a new website named `site2`, mapped its physical path to the new directory, and configured the binding to port **`8080`**.
- **Firewall Rule Provisioning:** To allow internal traffic to hit port 8080, an inbound firewall rule was added via administrative PowerShell:
  ```powershell
  New-NetFirewallRule -DisplayName "Inbound Port 8080" -Direction Inbound -Protocol TCP -LocalPort 8080 -Action Allow
