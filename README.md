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
# Root Cause Analysis: Windows DNS Resolution Failure

## Overview

One of the primary issues identified during this lab was a DNS resolution failure affecting the Windows 11 client. While communication with internal resources remained functional, the client was unable to resolve external domain names.

---

## Problem

Running the following command:

```powershell
nslookup google.com
```

returned a timeout error:

```
*** Request to UnKnown timed-out
DNS request timed out.
```

Despite this, the client could still communicate with internal systems on the network, indicating that basic network connectivity was intact.

---

## Root Cause

The Windows client was automatically prioritizing an **IPv6 link-local DNS server** advertised by the gateway. Because this DNS server was not configured to provide external name resolution, DNS queries failed before reaching the intended Active Directory DNS server.

The correct DNS server configured for the lab environment was:

```
192.168.10.20
```

---

## Resolution

To correct the issue:

- Disabled IPv6 on the Windows client network adapter.
- Ensured the client used the internal Active Directory DNS server (`192.168.10.20`) for name resolution.
- Renewed the network configuration and verified DNS settings.

---

## Validation

After the configuration change:

- `nslookup google.com` completed successfully.
- External domain names resolved correctly.
- Internet connectivity was restored.
- Internal network services continued to function normally.

---

## Skills Demonstrated

- DNS troubleshooting
- Windows network configuration
- IPv4/IPv6 diagnostics
- Root cause analysis
- Enterprise troubleshooting methodology
- Post-remediation validation

## Screenshots



### Lab Overview
<img width="672" height="640" alt="Image" src="https://github.com/user-attachments/assets/9b9e42bb-2218-44f5-91c8-a53ebb509b61" />

### Windows Performance Troubleshooting
<img width="672" height="531" alt="Image" src="https://github.com/user-attachments/assets/e1a40618-9fbc-4319-ada1-2433866580c4" />
<img width="673" height="530" alt="Image" src="https://github.com/user-attachments/assets/52c0d46e-d4fa-4703-9cc8-4865b8d96d63" />


### DNS Troubleshooting
<br><img width="422" height="606" alt="Image" src="https://github.com/user-attachments/assets/0bd90e9b-b938-41b0-8ed4-211b052d11bf" /></br>

<br><img width="421" height="569" alt="Image" src="https://github.com/user-attachments/assets/2b84034e-a7ac-47b1-951e-3edec8c9f4a4" /></br>

<br><img width="420" height="600" alt="Image" src="https://github.com/user-attachments/assets/2b9830ba-51c1-4e7b-b716-1bea21fdc2e6" /></br>

### DHCP Verification
<img width="421" height="637" alt="Image" src="https://github.com/user-attachments/assets/0be3af55-1f51-4443-8d5d-f2b6e2da4988" />

### Remote Support
<img width="421" height="651" alt="Image" src="https://github.com/user-attachments/assets/7b8e8dab-032a-4c88-9cdc-2f48f0b283e1" />




### Security and Final Validation
<img width="417" height="644" alt="Image" src="https://github.com/user-attachments/assets/31e44c04-fd4e-46d6-accb-f1a2ee2f1f34" />


