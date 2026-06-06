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

**Failed Windows Login Attempts**

Executed PowerShell with suspicious flags commonly seen in attacker behavior.

