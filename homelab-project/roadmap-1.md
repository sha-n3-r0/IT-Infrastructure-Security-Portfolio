# Homelab Security & Networking Journey Documentation

## Project Overview

This project was created to gain hands-on experience in networking, firewall administration, network segmentation, intrusion detection, and cybersecurity operations using a virtualized homelab environment.

### Infrastructure

```text
Proxmox VE
├── pfSense Firewall
├── Kali Linux
├── Ubuntu Server
├── Windows Server 2022
└── TrueNAS
```

### Network Architecture

```text
Internet
    ↓
ISP Router
    ↓
pfSense
├── LAN (192.168.10.0/24)
│   ├── Kali Linux
│   └── TrueNAS
│
└── OPT1 / LAB (192.168.20.0/24)
    ├── Ubuntu Server
    └── Windows Server 2022
```

---

# Phase 1 – Static DHCP Mappings

## Objective

Assign permanent IP addresses to critical devices using DHCP reservations.

## Tasks Performed

* Configured DHCP Static Mappings in pfSense
* Reserved IP addresses based on MAC addresses
* Verified devices received correct addresses

### Reserved Devices

| Device         | IP Address    |
| -------------- | ------------- |
| Kali Linux     | 192.168.10.30 |
| Ubuntu Server  | 192.168.20.10 |
| Windows Server | 192.168.20.11 |
| TrueNAS        | 192.168.10.40 |

## Skills Learned

* DHCP Concepts
* DHCP Reservations
* MAC Address Identification
* IP Address Planning
* Network Inventory Management

## Issues Encountered

* Devices receiving dynamic IPs
* Incorrect MAC address assignments

## Resolution

Verified MAC addresses and recreated DHCP mappings.

---

# Phase 2 – Firewall Rules

## Objective

Understand how pfSense processes firewall rules.

## Tasks Performed

* Created allow rules
* Created block rules
* Tested internet restrictions
* Tested source-based filtering

### Example Rule

```text
Block Ubuntu Internet Access
Source: 192.168.20.10
Destination: Any
Action: Block
```

## Skills Learned

* Rule Processing Order
* First Match Wins Concept
* Stateful Firewall Operation
* Traffic Filtering
* Access Control

## Issues Encountered

* Rule appeared ineffective

## Resolution

Discovered pfSense processes rules top-to-bottom and adjusted rule order.

---

# Phase 3 – Network Segmentation

## Additional Issues Encountered

### Inter-VLAN Communication Failure

Symptoms:

```text
Kali Linux could not communicate with devices on the LAB network.
```

Investigation:

* Verified IP addressing.
* Verified subnet masks.
* Verified pfSense interface assignments.

Resolution:

* Reviewed firewall rules between interfaces.
* Confirmed routing through pfSense.
* Adjusted allow/block policies.

### DHCP Not Assigning Addresses on OPT1

Symptoms:

```text
Devices connected to OPT1 received no IP address.
```

Resolution:

* Enabled DHCP Server on OPT1.
* Configured correct subnet range.
* Renewed client leases.

## Additional Skills Learned

* Inter-VLAN Routing
* Gateway Configuration
* DHCP Scope Management
* Network Isolation Design
* Security Zone Architecture

---

# Phase 4 – OpenVPN Remote Access (Partially Completed)

## Objective

Implement a secure remote access VPN solution using OpenVPN on pfSense to allow remote access to the homelab environment.

## Tasks Performed

### Certificate Infrastructure

Created:

```text
HomeVPN_CA
```

Purpose:

* Establish trust between VPN clients and server.
* Sign OpenVPN certificates.

Created:

```text
OpenVPN_Server Certificate
```

Purpose:

* Identify the VPN server.
* Enable SSL/TLS encryption.

Created:

```text
VPN User Certificate
```

Purpose:

* Authenticate VPN users.
* Restrict VPN access to authorized users only.

---

### OpenVPN Server Configuration

Configured:

```text
Protocol: UDP
Port: 1194
Tunnel Network: 10.8.0.0/24
Authentication:
SSL/TLS + User Authentication
```

Configured:

* OpenVPN Server
* User Authentication
* Certificate-Based Authentication
* Tunnel Network

---

### Firewall Configuration

Created WAN Firewall Rule:

```text
Allow UDP 1194
```

Created OpenVPN Interface Rule:

```text
Allow OpenVPN Clients
```

Verified:

* Firewall rule functionality
* OpenVPN interface accessibility

---

### Router Configuration

Configured TP-Link Port Forwarding:

```text
UDP 1194
→
192.168.1.108
```

Purpose:

* Forward VPN traffic from router to pfSense.

---

## Verification Performed

Verified:

```text
✓ OpenVPN Service Running
✓ Certificate Authority Functional
✓ Server Certificate Functional
✓ User Certificate Functional
✓ WAN Firewall Rule Present
✓ OpenVPN Rule Present
✓ Port Forwarding Configured
```

---

## Issues Encountered

### VPN Connection Timeout

Symptoms:

```text
VPN client unable to establish connection from mobile data.
```

Investigation:

* Verified OpenVPN service status.
* Verified firewall rules.
* Verified certificate configuration.
* Verified TP-Link port forwarding.

---

### Carrier Grade NAT (CGNAT)

Observed:

```text
TP-Link WAN Address:
10.10.10.x
```

Analysis:

The ISP assigned a private WAN address instead of a public IP address.

This prevented inbound VPN connections from reaching the OpenVPN server despite correct configuration.

---

## Skills Learned

### VPN Technologies

* OpenVPN Fundamentals
* Remote Access VPN Concepts
* VPN Authentication Methods
* VPN Tunnel Configuration

### Certificate Management

* Public Key Infrastructure (PKI)
* Certificate Authority Management
* Server Certificates
* User Certificates
* TLS Authentication

### Networking

* Port Forwarding
* NAT Concepts
* Double NAT Analysis
* WAN Connectivity Troubleshooting
* Remote Access Design

### Troubleshooting

* OpenVPN Diagnostics
* Service Verification
* Firewall Validation
* Network Path Analysis
* Root Cause Analysis

---

## Outcome

OpenVPN infrastructure was successfully deployed and validated internally.

Remote access testing could not be completed due to ISP Carrier Grade NAT (CGNAT).

The project remains partially completed until:

```text
□ Public IP Address Obtained
OR
□ ISP Bridge Mode Implemented
OR
□ Alternative VPN Solution Deployed
   (WireGuard / Tailscale)
```
---

# Phase 5 – Nmap Testing

## Objective

Generate reconnaissance traffic for Suricata analysis.

## Tests Performed

### SYN Scan

```bash
nmap -sS 192.168.20.10
```

### Service Detection

```bash
nmap -sV 192.168.20.10
```

### OS Detection

```bash
nmap -O 192.168.20.10
```

### Aggressive Scan

```bash
nmap -A 192.168.20.10
```

### Subnet Scan

```bash
nmap -Pn -sS 192.168.20.0/24
```

## Skills Learned

* Host Discovery
* Port Scanning
* Service Enumeration
* OS Fingerprinting
* Reconnaissance Methodology

## Issues Encountered

### Scan Signatures Not Triggering

Resolution:

Verified Suricata functionality through other alerts and determined scan traffic did not match active signatures.

---

# Phase 6 – Alert Analysis

## Objective

Learn how Security Operations Centers (SOC) analyze alerts.

## Sample Alerts

### ICMP Alert

```text
SURICATA ICMPv4 Unknown Code
```

### TCP Alert

```text
SURICATA STREAM Excessive Retransmissions
```

## Analysis Workflow

```text
Alert
 ↓
Source IP
 ↓
Destination IP
 ↓
Protocol
 ↓
SID
 ↓
Priority
 ↓
Verdict
```

## Skills Learned

* Alert Investigation
* Source/Destination Analysis
* SID Interpretation
* Priority Analysis
* False Positive Identification

## Example Finding

```text
Source:
192.168.20.11

Destination:
Internet Host

Alert:
SURICATA STREAM Excessive Retransmissions

Priority:
3

Verdict:
Low Risk / Informational
```

---

# Phase 7 – IPS Configuration

## Objective

Convert IDS monitoring into active blocking.

## Tasks Performed

Enabled:

```text
Block Offenders
```

Configured:

```text
IPS Mode: Legacy
Kill States: Enabled
Which IP to Block: BOTH
```

## Skills Learned

* IPS Concepts
* Automated Blocking
* Host Blocking
* Firewall State Management

## Issues Encountered

### No Nmap Blocks Generated

Resolution:

Determined Suricata was functioning correctly but active signatures did not match generated scans.

Verified through:

```text
Windows startup traffic
TCP alerts
ICMP alerts
```

---

# Additional Skills Acquired

## pfSense Administration

* Interfaces
* DHCP
* Firewall
* DNS
* Routing
* VPN Fundamentals

## Proxmox Administration

* VM Management
* Virtual Switches
* Network Bridges
* VM Networking

## Network Troubleshooting

* Routing Problems
* DHCP Issues
* Firewall Problems
* VPN Troubleshooting
* IDS Troubleshooting

## Cybersecurity Concepts

* Defense in Depth
* Network Segmentation
* IDS vs IPS
* Threat Detection
* Traffic Analysis
* Security Monitoring

---

# Current Status

```text
Completed:
✓ Static DHCP
✓ Firewall Rules
✓ Network Segmentation
✓ Suricata IDS
✓ Nmap Testing
✓ Alert Analysis
✓ IPS Configuration
```

---

# Future Roadmap

## Planned Projects

### OpenVPN Remote Access

Goal:

```text
Mobile Data
      ↓
OpenVPN
      ↓
pfSense
      ↓
Home Network
```

### Windows Active Directory

Learn:

* Domain Controllers
* DNS
* Group Policy
* User Management

### Wazuh SIEM

Learn:

* Log Aggregation
* Threat Detection
* Security Monitoring
* Incident Response

### WireGuard VPN

Learn:

* Modern VPN Technologies
* Remote Access
* Site-to-Site Tunnels

### Bridge Mode Migration

Future Target:

```text
ISP Modem
      ↓
pfSense
      ↓
Entire Network
```

---

# Final Reflection

This homelab project provided practical experience in networking, firewall management, intrusion detection, network segmentation, and cybersecurity operations. The environment successfully simulated a small enterprise network and established a strong foundation for future studies in System Administration, Networking, Security Operations (SOC), and Cybersecurity Engineering.

