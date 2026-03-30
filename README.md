Windows RDP Misconfiguration Lab

 Overview

This lab demonstrates how a misconfigured Windows 10 system exposing Remote Desktop Protocol (RDP) can lead to unauthorized access when weak credentials are used.

The objective of this project was to simulate a real-world penetration testing scenario involving enumeration, service discovery, and credential abuse.



 Objective

- Identify exposed services on a target system
- Enumerate potential entry points
- Gain access through weak authentication
- Document the full attack path



 Lab Setup

- Attacker Machine: Kali Linux
- Target Machine: Windows 10 (RDP enabled)
- Network: Bridged (same network)


  

STEP 1

Reconnaissance

Network Discovery

Performed a ping scan to identify live hosts:

nmap -sn <target-range>
https://github.com/vaibhavkrishna12004/windows-rdp-misconfiguration-lab/commit/e125700b654a1bfd81aaf02c8bf1f12e91ec5e22


STEP 2


Port Scanning

Identified open ports and services:

nmap -sV -sC <target-ip>
https://github.com/vaibhavkrishna12004/windows-rdp-misconfiguration-lab/commit/e125700b654a1bfd81aaf02c8bf1f12e91ec5e22#diff-9fae3f3df3f5d66fa47e596e15b1348e0d7e21ae977ae13c6e8e916e1a4bac53

Findings:

- Port 3389 (RDP) open
- Port 445 (SMB) open


STEP 3


Enumeration

SMB Enumeration

Checked for anonymous access and shares:

smbclient -L //<target-ip>
https://github.com/vaibhavkrishna12004/windows-rdp-misconfiguration-lab/commit/e125700b654a1bfd81aaf02c8bf1f12e91ec5e22#diff-9fae3f3df3f5d66fa47e596e15b1348e0d7e21ae977ae13c6e8e916e1a4bac53

Attempted further enumeration using:

enum4linux <target-ip>
https://github.com/vaibhavkrishna12004/windows-rdp-misconfiguration-lab/commit/e125700b654a1bfd81aaf02c8bf1f12e91ec5e22#diff-ac9af51bd54a562a6a81b1556f41d70e9c10839f92ff7b5495a06712e9e415c9


STEP 4

Directory Bruteforcing

Tested for web directories (if applicable):

dirb http://<target-ip>
https://github.com/vaibhavkrishna12004/windows-rdp-misconfiguration-lab/commit/e125700b654a1bfd81aaf02c8bf1f12e91ec5e22#diff-0d0d625350a8bf81ce85c2fb0815458119367f11bd73dad60fe4a3ef93fd5860



STEP 5

Initial Access

RDP Login Attempt

Used RDP client to attempt login:

xfreerdp /u:steven /p:steven /v:<target-ip>
https://github.com/vaibhavkrishna12004/windows-rdp-misconfiguration-lab/commit/e125700b654a1bfd81aaf02c8bf1f12e91ec5e22#diff-6293ea7128eef25fa8d5391ae74cfb811adaed7420e59683ad1b7cb6cc38d8a6


 Successfully gained access using weak credentials.



Vulnerability Identified

- Weak credentials (username/password)
- RDP exposed to network
- Lack of account lockout policy



Impact

An attacker can:

- Gain full remote access to the system
- Execute commands
- Access sensitive files
- Move laterally within the network



Mitigation

- Enforce strong password policies
- Disable RDP if not required
- Use Network Level Authentication (NLA)
- Implement account lockout mechanisms
- Restrict RDP access via firewall/VPN



Proof of Concept

Screenshots included:

- Nmap scan results
- SMB enumeration
- RDP login success



 Key Takeaways

This lab highlights how:

- Misconfigurations are often more dangerous than complex vulnerabilities
- Weak credentials remain a major security risk
- Proper enumeration is critical in penetration testing
