# Homelab Security & Networking Journey Documentation

## Project Overview

This project was created to gain hands-on experience in networking, firewall administration, network segmentation, intrusion detection, intrusion prevention, VPN technologies, and cybersecurity operations using a virtualized homelab environment.

---

## Infrastructure

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

| Device              | IP Address    |
| ------------------- | ------------- |
| Kali Linux          | 192.168.10.30 |
| Ubuntu Server       | 192.168.20.10 |
| Windows Server 2022 | 192.168.20.11 |
| TrueNAS             | 192.168.10.40 |

## Skills Learned

* DHCP Fundamentals
* DHCP Reservations
* MAC Address Identification
* IP Address Management
* Network Inventory Management

## Issues Encountered

### Dynamic IP Assignment

Symptoms:

```text
Devices received different IP addresses after reboot.
```

Resolution:

* Configured DHCP Static Mappings
* Verified MAC addresses
* Renewed DHCP leases

---

# Phase 2 – Firewall Rules

## Objective

Understand how pfSense processes and enforces firewall rules.

## Tasks Performed

* Created Allow Rules
* Created Block Rules
* Tested Internet Restrictions
* Tested Source-Based Filtering

### Example Rule

```text
Block Ubuntu Internet Access

Source:
192.168.20.10

Destination:
Any

Action:
Block
```

## Skills Learned

* Firewall Rule Processing
* Stateful Firewalls
* Rule Ordering
* Traffic Filtering
* Access Control

## Issues Encountered

### Rule Not Working

Symptoms:

```text
Traffic continued despite block rule.
```

Resolution:

* Learned "First Match Wins" principle
* Adjusted rule order
* Re-tested connectivity

---

# Phase 3 – Network Segmentation

## Objective

Separate devices into security zones using pfSense and Proxmox networking.

## Tasks Performed

### Created New Network

```text
vmbr2
```

### Added New pfSense Interface

```text
OPT1
```

### Assigned Devices

```text
Ubuntu Server
Windows Server 2022
```

to:

```text
192.168.20.0/24
```

### Enabled DHCP on OPT1

Configured:

```text
192.168.20.100 – 192.168.20.199
```

## Skills Learned

* Network Segmentation
* Security Zones
* Inter-Network Routing
* Virtual Switching
* Gateway Configuration
* DHCP Scope Management

## Issues Encountered

### Inter-Network Connectivity Failure

Symptoms:

```text
Kali could not communicate with LAB devices.
```

Resolution:

* Verified routing
* Verified firewall rules
* Adjusted OPT1 policies

### No Internet on LAB Devices

Symptoms:

```text
Windows Server received IP address but had no Internet access.
```

Resolution:

* Created OPT1 Allow Rule
* Enabled outbound communication
* Verified gateway configuration

---

# Phase 4 – OpenVPN Remote Access (Partially Completed)

## Objective

Implement secure remote access to the homelab using OpenVPN.

## Tasks Performed

### Certificate Infrastructure

Created:

```text
HomeVPN_CA
```

Created:

```text
OpenVPN Server Certificate
```

Created:

```text
VPN User Certificate
```

### OpenVPN Server Configuration

Configured:

```text
Protocol: UDP
Port: 1194
Tunnel Network: 10.8.0.0/24
```

### Firewall Configuration

Created:

```text
Allow UDP 1194
```

### Router Configuration

Configured TP-Link Port Forwarding:

```text
UDP 1194
→
pfSense WAN IP
```

## Skills Learned

* OpenVPN Deployment
* Certificate-Based Authentication
* PKI Concepts
* TLS Encryption
* Port Forwarding
* Remote Access Design
* VPN Troubleshooting

## Issues Encountered

### Remote Testing Not Completed

Reason:

```text
Mobile Data Testing Not Available
```

### Potential CGNAT Investigation

Observed:

```text
Private WAN addressing from ISP
```

Potential Impact:

```text
OpenVPN may be unreachable from the Internet.
```

## Current Status

```text
◐ PARTIALLY COMPLETED
```

Completed:

* Certificate Creation
* OpenVPN Server Configuration
* Firewall Rules
* Port Forwarding

Pending:

* Mobile Data Testing
* External Connectivity Validation
* CGNAT Verification

---

# Phase 5 – Suricata IDS Deployment

## Objective

Deploy and configure an Intrusion Detection System using Suricata.

## Tasks Performed

* Installed Suricata Package
* Enabled ET Open Rules
* Configured WAN Monitoring
* Configured OPT1 Monitoring
* Downloaded and Updated Rule Sets
* Verified Alert Generation

## Skills Learned

* IDS Concepts
* Signature-Based Detection
* Threat Intelligence Feeds
* Traffic Inspection
* Security Monitoring

## Issues Encountered

### Rule Category Confusion

Symptoms:

```text
Expected beginner feeds were not available.
```

Resolution:

Learned modern Suricata versions use ET Open rule categories.

---

# Phase 6 – Nmap Testing

## Objective

Generate reconnaissance traffic for IDS testing.

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

### Network Sweep

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

Verified Suricata functionality through other alerts and determined active scans did not match loaded signatures.

---

# Phase 7 – Alert Analysis

## Objective

Learn SOC-style alert investigation and interpretation.

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
* Event Validation
* False Positive Identification

## Example Finding

```text
Source:
192.168.20.11

Alert:
SURICATA STREAM Excessive Retransmissions

Priority:
3

Verdict:
Informational / Low Risk
```

---

# Phase 8 – IPS Configuration (Partially Completed)

## Objective

Convert IDS monitoring into active prevention.

## Tasks Performed

Enabled:

```text
Block Offenders
```

Configured:

```text
IPS Mode: Legacy
Kill States: Enabled
Block: BOTH
```

## Skills Learned

* IDS vs IPS
* Automated Blocking
* Host Blocking
* Stateful Session Termination
* Prevention Concepts

## Issues Encountered

### No Block Events Generated

Symptoms:

```text
Nmap scans did not trigger blocking actions.
```

Resolution:

Confirmed:

* Suricata Running
* Alerts Generated
* Traffic Inspected

Conclusion:

```text
Rule tuning required.
```

## Current Status

```text
◐ PARTIALLY COMPLETED
```

Completed:

* IPS Configuration
* Block Offenders
* Alert Verification

Pending:

* Successful Block Event
* Rule Tuning
* Block Validation Testing

---

# Current Project Status

## Completed

```text
✓ Static DHCP Mappings
✓ Firewall Rules
✓ Network Segmentation
✓ Suricata IDS Deployment
✓ Nmap Testing
✓ Alert Analysis
```

## Partially Completed

```text
◐ OpenVPN Remote Access
◐ Suricata IPS Configuration
```

---

# Skills Acquired

## Networking

* DHCP Administration
* DHCP Reservations
* Routing
* NAT Concepts
* Port Forwarding
* Gateway Configuration
* Network Segmentation

## Firewall Administration

* pfSense Administration
* Firewall Rule Management
* Stateful Firewalls
* Traffic Control

## Virtualization

* Proxmox Administration
* Virtual Networking
* Linux Bridges (vmbr)
* Multi-Network Architecture

## VPN Technologies

* OpenVPN Deployment
* Certificate Management
* PKI Concepts
* Remote Access Architecture

## Cybersecurity

* IDS Deployment
* IPS Fundamentals
* Security Monitoring
* Reconnaissance Techniques
* Traffic Analysis

## Security Operations

* Alert Investigation
* Event Analysis
* False Positive Identification
* Security Monitoring Workflows

## Troubleshooting

* DHCP Issues
* Routing Issues
* Firewall Issues
* VPN Connectivity Issues
* IDS/IPS Troubleshooting

---

# Future Roadmap

## Phase 9 – Windows Active Directory

Learn:

* Active Directory
* DNS
* Group Policy
* User Management
* Organizational Units

## Phase 10 – Wazuh SIEM

Learn:

* Log Aggregation
* Detection Engineering
* Threat Hunting
* Incident Response

## Phase 11 – ISP Bridge Mode & Full pfSense Deployment

Target:

```text
ISP Modem (Bridge Mode)
          ↓
pfSense
          ↓
Entire Network
```

## Phase 12 – OpenVPN Completion

Complete:

* Mobile Data Testing
* External Connectivity Validation
* Remote Access Verification

---

# Final Reflection

This homelab project provided practical experience in networking, firewall administration, VPN technologies, network segmentation, intrusion detection, intrusion prevention, traffic analysis, and cybersecurity operations. The environment successfully simulated a small enterprise network and established a strong foundation for future growth in System Administration, Network Engineering, Security Operations (SOC), and Cybersecurity.
