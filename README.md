# FTP-Credential-Capture-and-Secure-Migration
This demonstrates how insecure FTP credentials can be intercepted using Wireshark and tcpdump, followed by a secure migration to SFTP using SSH encryption. The lab includes network reconnaissance with Nmap, packet analysis, plaintext credential capture, encrypted traffic validation, and security impact analysis in a controlled virtual environment.

# FTP to SFTP Security Migration Lab

## Overview

This project demonstrates the security risks associated with using FTP for file transfers and how migrating to SFTP significantly improves security by encrypting authentication and data transmission.

The lab was performed inside a controlled virtual environment using Kali Linux and Windows 11 virtual machines. Network reconnaissance, packet capture, and protocol analysis were used to demonstrate how FTP credentials can be intercepted in plaintext and how SSH-based SFTP protects against credential theft.

---

# Objectives

- Demonstrate FTP credential interception
- Analyze insecure network traffic
- Perform reconnaissance using Nmap
- Capture packets using tcpdump and Wireshark
- Migrate from FTP to SFTP
- Validate encrypted communications
- Analyze security improvements after migration

---

# Lab Environment

## Virtual Machines Used

### Windows 11
- Configured as FTP server using IIS
- Later migrated to SFTP using OpenSSH

### Kali Linux
- Used for reconnaissance
- Packet capture
- Monitoring
- Security analysis

---

# Network Configuration

- Host-only network
- Isolated internal environment
- DHCP enabled
- No internet exposure

## IP Addressing

| System | Role | IP Address |
|---|---|---|
| Windows 11 | FTP/SFTP Server | 192.168.56.101 |
| Kali Linux | Monitoring System | 192.168.56.102 |

---

# Tools Used

- Nmap
- Wireshark
- tcpdump
- OpenSSH
- IIS FTP Server
- Oracle VirtualBox
- Kali Linux

---

# Reconnaissance

## Host Discovery

```bash
sudo nmap -sn 192.168.56.0/24
```

This scan was used to identify active systems within the sandbox environment.

### Discovered Hosts
- 192.168.56.101 — Windows FTP Server
- 192.168.56.102 — Kali Linux

---

# FTP Port Verification

## Scan FTP Port

```bash
sudo nmap -p 21 192.168.56.101
```

### Result

```text
21/tcp open ftp
```

This confirmed that the FTP service was exposed and accessible.

---

# FTP Credential Capture

## tcpdump Packet Capture

```bash
sudo tcpdump -i eth0 port 21 -A
```

### Purpose
This capture demonstrated that FTP transmits usernames and passwords in plaintext.

### Observation
The USER and PASS commands were visible directly inside captured packets.

This confirms that FTP does not provide encryption for authentication traffic.

---

# Wireshark Analysis

## Filter Used

```text
tcp.port == 21
```

Wireshark packet inspection clearly displayed readable authentication credentials within the FTP traffic.

This demonstrated the security risks associated with unencrypted legacy protocols.

---

# OS Detection

## Nmap Service & OS Detection

```bash
sudo nmap -sS -sV -O -Pn 192.168.56.101
```

### Purpose
- Service version detection
- Operating system fingerprinting
- Enumeration of exposed services

---

# Migration to SFTP

## Security Improvements Implemented

- Installed OpenSSH Server
- Enabled SSH service
- Updated firewall rules
- Disabled FTP service

The migration ensured that authentication and file transfers were encrypted using SSH.

---

# SFTP Verification

## Port Validation

```bash
sudo nmap -p 21,22 192.168.56.101
```

### Result

```text
21/tcp filtered ftp
22/tcp open ssh
```

This confirmed that FTP had been disabled and only encrypted SSH access remained available.

---

# Encrypted Traffic Validation

## tcpdump Analysis

```bash
sudo tcpdump -i eth0 port 22 -A
```

### Observation

Captured packets contained encrypted SSH traffic.

No usernames or passwords were visible during packet inspection.

---

# Wireshark SFTP Analysis

## Filter Used

```text
tcp.port == 22
```

Wireshark confirmed that all communication was encrypted using SSHv2.

This demonstrated secure authentication and encrypted data transmission.

---

# Security Impact Analysis

## FTP Risks

FTP credentials captured during packet analysis could allow attackers to:
- Gain unauthorized access
- Download sensitive files
- Modify server content
- Perform lateral movement
- Reuse credentials on other services

---

# Security Improvements After Migration

After migrating to SFTP:
- Authentication traffic became encrypted
- Credentials could no longer be intercepted
- Attack surface was reduced
- Passive sniffing attacks were mitigated

---

# Key Security Lessons

- FTP is insecure because it transmits credentials in plaintext
- Legacy protocols should be replaced with encrypted alternatives
- Packet capture tools can easily expose weak protocols
- SFTP significantly improves confidentiality and security
- Network validation and testing are essential after remediation

---

# Skills Demonstrated

- Network Reconnaissance
- Packet Analysis
- Protocol Analysis
- Credential Interception
- Linux Security Tools
- Nmap Scanning
- Wireshark Analysis
- SSH/SFTP Hardening
- Security Validation
- Risk Analysis

---

# Screenshots

## Included Screenshots
- FTP service verification
- Nmap reconnaissance scans
- tcpdump FTP credential capture
- Wireshark plaintext credentials
- OpenSSH installation
- SFTP login validation
- Encrypted SSH traffic analysis

---

# Disclaimer

This project was performed in a controlled lab environment for educational and authorized security testing purposes only.

---

# Author

Nicholas Dcunha
Cybersecurity Student | IT Support | Security Operations Enthusiast
