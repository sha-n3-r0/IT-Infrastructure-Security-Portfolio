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

## Objective

Separate systems into security zones.

## Tasks Performed

### Created New Proxmox Bridge

```text
vmbr2
```

### Created New pfSense Interface

```text
OPT1
```

### Assigned Lab Devices

```text
Ubuntu Server
Windows Server
```

to

```text
192.168.20.0/24
```

## Skills Learned

* Network Segmentation
* Layer 3 Routing
* Virtual Networking
* Proxmox Bridges
* Security Zones

## Issues Encountered

### Windows Server No Internet

Symptoms:

```text
Windows received IP but had no Internet access
```

Resolution:

* Verified gateway
* Verified DHCP
* Corrected virtual NIC configuration

---

# Phase 4 – Suricata IDS Deployment

## Objective

Deploy Intrusion Detection System using Suricata.

## Tasks Performed

* Installed Suricata Package
* Assigned Suricata to OPT1
* Downloaded ET Open Rules
* Enabled Rule Categories
* Verified Alert Generation

## Skills Learned

* IDS Concepts
* Signature-Based Detection
* Threat Intelligence Feeds
* Rule Categories
* Traffic Inspection

## Issues Encountered

### Missing Beginner Feed

Resolution:

Learned newer versions use ET Open categories instead of beginner feeds.

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

