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


  



Reconnaissance


Reconnaissance is the initial phase of a penetration test where information about the target system or network is gathered.
It helps identify active hosts, open ports, and services to understand potential attack surfaces


Performed a ping scan to identify live hosts:

nmap -sn <target-IP> helps us identify which systems on the network are active.
<img width="1920" height="1080" alt="Nmap -sn " src="https://github.com/user-attachments/assets/3589bf13-2b8e-4a28-82ad-c1a1896c0194" />







Port Scanning

Port scanning identifies open ports and detects services running on them.
This helps determine potential entry points and technologies used by the target system.

nmap -sV -sC <target-IP> this Identifies open ports, detects the services running on those ports and gathers additiona information.
<img width="1920" height="1080" alt="Nmap -sV -sC" src="https://github.com/user-attachments/assets/0717665f-b384-4287-889c-4c24fd9aaf89" />

- Port 3389 (RDP) open
- Port 445 (SMB) open
- Port 5357 (http) open


  
HTTP LOGIN

Perfomed a quick check of the IP over a search engine
<img width="1922" height="1047" alt="Http login check" src="https://github.com/user-attachments/assets/fe6bd490-9b2a-4b86-a43c-d745078c47cc" />








Enumeration

SMB enumeration involves listing shared resources available on a target system.
It helps identify misconfigured shares or unauthorized access possibilities.


Checked for anonymous access and shares:

smbclient -L //<target-ip>his helps us identify shared folders and check if anonymous access id allowed, (sometimes it is).
<img width="1920" height="1045" alt="smb guest login" src="https://github.com/user-attachments/assets/e229697c-81bd-4544-8720-63b8da4f35d9" />


Attempted further enumeration using: Advanced SMB enumeration gathers detailed information such as users, groups, and system data.
It is used to identify valid usernames and potential attack vectors within SMB services.

enum4linux <target-ip> This gathers details such as users, shares, groups, and system information crucial for attack.
<img width="1920" height="1045" alt="smbclient and enumlinux" src="https://github.com/user-attachments/assets/78ddce90-256f-4cf9-a0c2-cca5d1fffcb4" />






Directory Bruteforcing

Directory brute forcing is used to discover hidden files and directories on a web server.
It helps uncover sensitive endpoints like admin panels or backup files.

dirb http://<target-ip> This helps identify hidden directories and files that are not directly accessible through the website.
<img width="1920" height="1045" alt="dirb check" src="https://github.com/user-attachments/assets/29becce8-5b0e-422e-be11-8a65b83ad638" />








Initial Access

Remote Desktop Protocol Login Attempt

Used RDP client to attempt login: RDP access allows remote login to a system using the Remote Desktop Protocol.
It can lead to full system control if valid credentials are obtained.

xfreerdp /u:steven /p:steven /v:<target-ip> this gained us login through the port 3389 with the help of weak credentials of the user.
<img width="1920" height="1045" alt="xfreerdp1" src="https://github.com/user-attachments/assets/634ef28f-76e9-4506-bb58-52fe9c752a02" />

The port gave us full access to the system.
<img width="1034" height="804" alt="RDP exploit with xfreerdp" src="https://github.com/user-attachments/assets/9c268528-e296-46c7-9064-56ea7e3d2911" />



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



Conclusion

This assessment demonstrated how exposed services such as SMB and RDP
can be analyzed for potential vulnerabilities.

While SMB enumeration did not reveal misconfigurations, weak credentials
allowed successful access via RDP, highlighting the risk of poor authentication practices.

This emphasizes the importance of strong password policies and restricted remote access.
