# Homelab Roadmap 2

# Enterprise Systems Administration & Security Operations

This roadmap builds upon the networking and cybersecurity foundation established in **Homelab-R1**. The focus shifts toward enterprise Windows infrastructure, identity management, centralized administration, and Security Operations Center (SOC) technologies.

The lab continues to be hosted on **Proxmox VE**, utilizing Windows Server 2022, Windows 11 Pro, Ubuntu Server, pfSense, and additional security platforms to simulate a real-world enterprise environment.

---

# Current Project Status

## Completed

```text
✓ Windows Server 2022 Installation
✓ Windows Server Network Configuration
✓ Active Directory Domain Services (AD DS)
✓ Domain Controller Promotion
✓ Domain Creation (shanero.com)
✓ DNS Server Configuration
✓ Windows 11 Pro Deployment
✓ Windows 11 Domain Join
✓ Active Directory Computer Management
```

## Partially Completed

```text
◐ Organizational Unit (OU) Design
◐ User and Group Management
```

## Not Started

```text
□ Group Policy Objects (GPO)
□ Shared Folder & NTFS Permissions
□ Domain Authentication Policies
□ Wazuh SIEM Deployment
□ Enterprise Network Deployment
```

---

# Skills Acquired

## Windows Server Administration

- Windows Server 2022 Installation
- Server Configuration
- Static IP Configuration
- Server Renaming
- Role & Feature Installation
- DNS Server Administration
- Domain Controller Deployment

## Active Directory

- Active Directory Domain Services
- Forest Creation
- Domain Creation
- Domain Controller Promotion
- Active Directory Users & Computers
- Computer Object Management
- Domain Join
- Domain Authentication

## Client Administration

- Windows 11 Deployment
- Domain Client Configuration
- Enterprise Workstation Setup
- DNS Configuration
- Client Authentication
- Virtual Machine Administration

## Virtualization

- Proxmox VE Administration
- Windows Virtual Machine Deployment
- VirtIO Driver Installation
- Virtual Hardware Optimization
- Resource Allocation
- Network Integration

## Troubleshooting

- DNS Resolution Issues
- Domain Join Failures
- Windows Networking
- Active Directory Connectivity
- Virtual Machine Performance
- VirtIO Driver Configuration

---

# Project Roadmap

## Phase 1 – Windows Server Deployment

- Windows Server 2022 Installation
- Static IP Configuration
- Server Renaming
- Windows Update
- Initial Server Configuration
- DNS Configuration

---

## Phase 2 – Active Directory Domain Services

- AD DS Installation
- Domain Controller Promotion
- Forest Creation
- Domain Creation (shanero.com)
- DNS Integration
- Domain Validation

---

## Phase 3 – Enterprise Client Deployment

- Windows 11 Pro Installation
- VirtIO Driver Installation
- Network Configuration
- DNS Configuration
- Domain Join
- Active Directory Verification

---

## Phase 4 – Active Directory Administration *(Partially Completed)*

- Organizational Unit (OU) Design
- User Creation
- Security Groups
- Group Management
- Computer Organization
- Administrative Delegation *(Pending)*

---

## Phase 5 – Group Policy Management

- Group Policy Objects (GPO)
- Password Policy
- Account Lockout Policy
- Windows Update Policy
- Desktop Restrictions
- Drive Mapping
- Security Policies

---

## Phase 6 – File Services

- Shared Folder Configuration
- NTFS Permissions
- Share Permissions
- Access-Based Enumeration
- Network Drive Mapping
- File Access Testing

---

## Phase 7 – Wazuh SIEM

- Ubuntu Server Preparation
- Wazuh Manager Installation
- Wazuh Dashboard
- Filebeat Configuration
- Windows Agent Deployment
- Linux Agent Deployment
- pfSense Log Integration
- Security Event Collection
- Threat Detection
- Alert Monitoring

---

## Phase 8 – Enterprise Infrastructure

- Enterprise User Management
- Security Hardening
- Active Directory Best Practices
- Backup Strategy
- Disaster Recovery Planning
- Enterprise Documentation

---

# Challenges Encountered

Unlike many Windows Server tutorials that use Oracle VirtualBox, this homelab is built entirely on **Proxmox VE** with an existing segmented network architecture.

Integrating Active Directory into an already established environment required adapting the implementation rather than simply following the tutorial step by step.

Challenges included:

- Translating VirtualBox networking into Proxmox networking
- Integrating Windows Server into the existing lab network
- Configuring DNS correctly for Active Directory
- Joining Windows 11 to the domain
- Troubleshooting Windows virtual machine performance
- Learning and installing VirtIO drivers for improved VM performance

These challenges strengthened my troubleshooting abilities and reinforced the importance of understanding concepts rather than relying solely on tutorials.

---

# Lessons Learned

This project introduced me to enterprise identity management using Microsoft Active Directory.

Key takeaways include:

- Understanding how Active Directory manages users and computers
- The critical role DNS plays within Active Directory
- How Windows clients discover Domain Controllers
- The domain join process
- Enterprise workstation administration
- Windows Server role management
- Planning enterprise infrastructure before deployment

One of the most rewarding milestones was successfully joining my Windows 11 virtual machine to the **shanero.com** domain and seeing it appear inside **Active Directory Users and Computers**.

This experience greatly increased my confidence in Windows Server administration and encouraged me to continue learning enterprise infrastructure technologies.

---

# Final Reflection

Homelab-R2 marks the transition from networking and cybersecurity into enterprise systems administration.

Building upon the infrastructure created in Homelab-R1, this phase focuses on centralized identity management, Windows Server administration, enterprise workstation deployment, and future Security Operations (SOC) technologies.

The roadmap will continue with Group Policy management, enterprise file services, Wazuh SIEM deployment, and infrastructure hardening, providing practical experience aligned with Systems Administration, Infrastructure Engineering, and Cybersecurity career paths.
