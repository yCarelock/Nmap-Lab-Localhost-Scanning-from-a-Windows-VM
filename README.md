# Nmap-Lab-Localhost-Scanning-from-a-Windows-VM

⚔️ Goal: Using Nmap inside a controlled Windows 10 virtual machine to identify open ports and assess potential security risks.


🧰 Tools You’ll Use:
Your current Windows 10 VM

Nmap for Windows

Command Prompt or PowerShell

1. Install Nmap for Windows
Go to https://nmap.org/download.html

Download the Nmap Windows Installer

Run it with default options (includes nmap.exe and Zenmap GUI)

🔍 Localhost Port Scanning
Ran a basic Nmap scan against your own machine:

powershell:
nmap 127.0.0.1

![image](https://github.com/user-attachments/assets/8e40ba08-7ce8-4a4a-9794-f3d59c4360ca)


✅ What Just Happened:
I scanned the VM itself (127.0.0.1 = localhost).

🔍 What Nmap Found:
Port	State	Service
135	Open	msrpc
445	Open	microsoft-ds

These are typical Windows services:

Port 135 (msrpc) – Used for remote procedure calls (can be abused for lateral movement).

Port 445 (microsoft-ds) – Used for SMB (file sharing); common target for exploits like EternalBlue.

⚠️ Warning Message:
"Could not import all necessary Npcap functions..."

That just means raw packet capture mode isn’t available. Nmap falls back to "connect scan" (slower but still works). If you want full features later, install Npcap from

🧠 Contextual Interpretation
I recognized the security implications of:

Port 3389 (Remote Desktop Protocol): risk of unauthorized remote access.

Port 445 (SMB): commonly exploited by malware (e.g., WannaCry via EternalBlue).

![image](https://github.com/user-attachments/assets/df63be57-3f16-4f48-a8af-5782f35141cc)

Opened Windows Features to check SMB 1.0/CIFS status to understand legacy exposure risks.

![image](https://github.com/user-attachments/assets/72cb3ffa-9ae7-4f08-b7b2-505b56d84360)

💻 PowerShell Risk Output
Simulated a basic incident alert using PowerShell:

powershell

Write-Host "Port 3389 open – RDP enabled"
Write-Host "Port 139/445 open – SMB exposed (potential EternalBlue risk)"
This mimics the kind of output a junior SOC analyst might include in a scan report or ticket.

✅ Outcome
I successfully:

Performed a port scan using Nmap on a VM.

Identified and interpreted results.

Flagged risks associated with open ports.

Used PowerShell to simulate a detection/reporting step.
