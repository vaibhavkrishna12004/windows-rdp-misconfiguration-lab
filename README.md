Windows RDP Misconfiguration Lab

Overview
This project demonstrates how a misconfigured Windows 10 system exposing RDP can lead to unauthorized access.

The lab was built using:
- Kali Linux (attacker)
- Windows 10 VM (target)


Steps Performed

1. Network discovery using Nmap
2. SMB enumeration using enum4linux
3. Identified possible usernames
4. Enabled and accessed RDP service
5. Logged into the system using weak credentials



Skills Demonstrated
- Network Scanning (Nmap)
- Enumeration (SMB, enum4linux)
- Understanding misconfigurations
- Remote access via RDP
- Basic penetration testing workflow


Key Learning
Misconfigured services + weak credentials can easily lead to system compromise.
creenshots

### 🔍 Nmap Scan
![Nmap](KALI%20Windows%2010/Nmap%20-sV%20-sC.png)

### 🔎 SMB Enumeration
![SMB](KALI%20Windows%2010/smbclient%20and%20enumlinux.png)

### 🌐 HTTP Check
![HTTP](KALI%20Windows%2010/Http%20login%20check.png)

### 📁 Directory Scan
![DIRB](KALI%20Windows%2010/dirb%20check.png)

### 🔐 RDP Access
![RDP](KALI%20Windows%2010/xfreerdp1.png)

### 🔓 Successful Login
![Access](KALI%20Windows%2010/RDP%20exploit%20with%20xfreerdp.png)
