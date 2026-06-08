# Wazuh SIEM Detection Lab
Tools: Oracle VirtualBox, Wazuh, Sysmon, Kali Linux, Windows 11, Ubuntu Server

Build a local SIEM detection lab using Wazuh to monitor a Windows 11 endpoint for suspicious activity. Deployed a Wazuh server on Ubuntu Server, installed the Wazuh agent and Sysmon on a Windows 11 VM, and used a Kali Linux VM to simulate attacker activity. Collected Windows Security logs, Sysmon process events, and File Integrity Monitoring alerts to investigate suspicious PowerShell execution, failed logins, file changes, and network reconnaissance.

# Architecture:

Oracle VirtualBox

Ubuntu Server -> Wazuh Manager, Wazuh Dashboard, Wazuh Indexer

Windows 11 VM -> Wazuh Agent, Sysmon

Kali Linux VM -> Nmap

# Detection Scenarios
**Failed Windows Login Attempts**

Generated failed login attempts on the Windows 11 endpoint and verified that Wazuh collected Windows Security events.

Event ID: 4625 

Log Source: Windows Security 

Detection Type: Failed Logon

**Suspicious Powershell Execution**

Executed PowerShell with suspicious flags commonly seen in attacker behavior.

```kql
powershell -ExecutionPolicy Bypass -NoProfile -Command "whoami; hostname; ipconfig; net user"
```
Mapped behavior to MITRE ATT&CK:

T1059.001 - Command and Scripting Interpreter: PowerShell
T1033 - System Owner/User Discovery
T1082 - System Information Discovery
T1087 - Account Discovery

**Sysmon Process Monitoring**

Configured Sysmon on the Windows 11 VM using the SwiftOnSecurity Sysmon configuration and forwarded Sysmon logs to Wazuh.

**File Integrity Monitoring**

Configured Wazuh File Integrity Monitoring to detect file creation, modification, and deletion in a test directory.

**Network Reconnaissance from Kali Linux**

Used Kali Linux to simulate network reconnaissance against the Windows 11 endpoint.
```kql
nmap -sV <192.168.10.20>
```
Mapped behavior to MITRE ATT&CK:

T1046 - Network Service Discovery

# Results
Detected Windows Security Event ID 4625 failed login attempts

Collected Sysmon process creation events from the Windows 11 endpoint

Detected suspicious PowerShell activity using Wazuh and Sysmon

Configured File Integrity Monitoring to alert on file creation, modification, and deletion

Simulated network reconnaissance from Kali Linux using Nmap

Practiced SOC-style investigation using Wazuh alerts and event logs
