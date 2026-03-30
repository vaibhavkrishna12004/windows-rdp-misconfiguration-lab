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
<img width="1920" height="1080" alt="Nmap -sn " src="https://github.com/user-attachments/assets/3589bf13-2b8e-4a28-82ad-c1a1896c0194" />

HTTP LOGIN

Perfomed a quick check of the IP over a search engine
<img width="1922" height="1047" alt="Http login check" src="https://github.com/user-attachments/assets/fe6bd490-9b2a-4b86-a43c-d745078c47cc" />



STEP 2


Port Scanning

Identified open ports and services:

nmap -sV -sC <target-ip>
<img width="1920" height="1080" alt="Nmap -sV -sC" src="https://github.com/user-attachments/assets/0717665f-b384-4287-889c-4c24fd9aaf89" />



Findings:

- Port 3389 (RDP) open
- Port 445 (SMB) open


STEP 3


Enumeration

SMB Enumeration

Checked for anonymous access and shares:

smbclient -L //<target-ip>
<img width="1920" height="1045" alt="smb guest login" src="https://github.com/user-attachments/assets/e229697c-81bd-4544-8720-63b8da4f35d9" />


Attempted further enumeration using:

enum4linux <target-ip>
<img width="1920" height="1045" alt="smbclient and enumlinux" src="https://github.com/user-attachments/assets/78ddce90-256f-4cf9-a0c2-cca5d1fffcb4" />


STEP 4

Directory Bruteforcing

Tested for web directories (if applicable):

dirb http://<target-ip>
<img width="1920" height="1045" alt="dirb check" src="https://github.com/user-attachments/assets/29becce8-5b0e-422e-be11-8a65b83ad638" />




STEP 5

Initial Access

RDP Login Attempt

Used RDP client to attempt login:

xfreerdp /u:steven /p:steven /v:<target-ip>
<img width="1920" height="1045" alt="xfreerdp1" src="https://github.com/user-attachments/assets/634ef28f-76e9-4506-bb58-52fe9c752a02" />



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
