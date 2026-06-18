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

# Phase 4 – OpenVPN Remote Access

## Objective

Implement secure remote access to the homelab environment using OpenVPN.

## Tasks Performed

* Created Internal Certificate Authority
* Generated Server Certificate
* Generated User Certificate
* Configured OpenVPN Server
* Configured WAN Firewall Rules
* Configured OpenVPN Firewall Rules
* Configured TP-Link Port Forwarding

## Verification

Verified:

✓ OpenVPN Service Running

✓ Certificate Authentication Working

✓ Firewall Rules Applied

✓ Port Forwarding Configured

## Issues Encountered

### VPN Connection Timeout

Symptoms:

```text
VPN client unable to establish connection from mobile data.
```

Investigation:

* Verified OpenVPN service status.
* Verified firewall rules.
* Verified TP-Link port forwarding.
* Verified certificates.

Resolution:

Discovered ISP assigned a private WAN address:

```text
10.10.10.x
```

Identified Carrier Grade NAT (CGNAT) preventing inbound VPN connectivity.

## Skills Learned

* Public Key Infrastructure (PKI)
* Certificate Management
* TLS Authentication
* Remote Access VPN
* Port Forwarding
* NAT Concepts
* Double NAT Troubleshooting
* CGNAT Identification
* Network Path Analysis

## Outcome

Successfully deployed OpenVPN infrastructure and identified ISP-level limitations preventing external connectivity.

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

