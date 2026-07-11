#  IT Troubleshooting Lab

## Project Overview
This hands-on enterprise troubleshooting lab demonstrates structured incident investigation across Windows and Linux systems in a small business environment. 

The lab simulates real-world operational issues that an IT Support Technician or Junior System Administrator must diagnose and resolve within a controlled virtual environment.

---

## Key Skills Demonstrated
* Cross-platform troubleshooting (Windows and Linux)
* DNS diagnostics and configuration
* Network connectivity testing and DHCP verification
* Remote administration via SSH
* Structured troubleshooting methodology
* Root cause analysis, corrective action, and final validation

---

## Lab Environment

### Infrastructure
* Domain Name: lab.local
* Subnet: 192.168.10.0/24

### Device Inventory
| Device Name | Operating System | IP Address | Role / Function |
| :--- | :--- | :--- | :--- |
| pfSense | pfSense Firewall | 192.168.10.1 | Default Gateway |
| WIN11-CLI-A | Windows 11 | 192.168.10.10 | Client Workstation |
| DC01 | Windows Server 2025 | 192.168.10.20 | Domain Controller / DNS / DHCP |
| UBUNTU-SRV | Ubuntu Server | 192.168.10.30 | Remote Server |
| UBUNTU-DSK | Ubuntu Desktop | 192.168.10.40 | Linux Client Workstation |

---

## Technologies Used
* Windows Server 2025
* Active Directory Domain Services (AD DS)
* DNS & DHCP Services
* Windows 11
* Ubuntu Server & Desktop
* pfSense Firewall
* SSH
* UTM Virtualization

---

## Troubleshooting Scenarios & Root Cause Analysis

### 1. Windows Client Performance Issue
Investigated slow system performance on the Windows 11 client by analyzing resource utilization in Task Manager and reviewing diagnostic evidence within Event Viewer.

### 2. DNS Resolution Failure
* **Problem:** `nslookup google.com` timed out on the Windows client, preventing external web browsing even though internal local network systems remained reachable.
* **Root Cause:** The client machine automatically prioritized an IPv6 link-local DNS address advertised by the gateway, which was not configured to handle external DNS resolution.
* **Resolution:** Disabled IPv6 on the client's network adapter, forcing all DNS queries to route directly to the internal Active Directory DNS server (`192.168.10.20`). This successfully restored external name resolution.

### 3. DHCP Service Verification
Reviewed the active operational state of the DHCP service on the Windows Server and verified correct lease assignment behavior to client devices.

### 4. Remote Server Support via SSH
Established secure remote command-line access to the Ubuntu Server instance from a client machine and verified the status and configuration of the SSH daemon.

### 5. Security and Final Validation
Confirmed ongoing firewall protection states across the architecture and validated network wide functionality following all corrective actions.

---

## Screenshots

### Lab Overview
![Lab Overview](screenshots/lab-overview.png)

### Windows Performance Troubleshooting
![Windows Performance Troubleshooting](screenshots/performance-troubleshooting.png)

### DNS Troubleshooting
![DNS Troubleshooting](screenshots/dns-troubleshooting.png)

### DHCP Verification
![DHCP Verification](screenshots/dhcp-verification.png)

### Remote Support
![Remote Support](screenshots/remote-support.png)

### Security and Final Validation
![Security and Final Validation](screenshots/security-validation.png)
