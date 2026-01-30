# Hack The Box – Tactics (Starting Point)

## Overview

**Tactics** is a *Starting Point* machine on Hack The Box designed to introduce core concepts related to **Windows enumeration**, **SMB services**, and **remote command execution** using common offensive security tools.  
The lab focuses on identifying SMB exposure, enumerating network shares, retrieving files, and gaining an interactive shell via Impacket.

---

## Machine Information

- **Difficulty:** Starting Point  
- **Category:** Windows / Network  
- **Platform:** Hack The Box  
- **Key Topics:**  
  - Nmap host discovery bypass  
  - SMB enumeration  
  - Administrative shares  
  - File retrieval via SMB  
  - Remote command execution (Impacket)

---

## Enumeration Summary

### Host Discovery

ICMP echo requests are blocked by the Windows firewall. To ensure the host is scanned regardless of ping response, host discovery is disabled during scanning.

- **Nmap switch used:** `-Pn`

---

### Service Enumeration

Enumeration reveals the presence of the **SMB (Server Message Block)** service.

- **SMB Protocol:** Server Message Block  
- **SMB Port:** `445/TCP`

---

## SMB Enumeration

### Listing Available Shares

The SMB service is queried to enumerate available network shares.

- **smbclient flag used:** `-L`  
- **Purpose:** List available SMB shares on the target

---

### Administrative Shares

Administrative shares are identified by a special character.

- **Administrative share indicator:** `$`
- **Accessible administrative share:** `C$`

The `C$` share provides access to the entire filesystem of the target machine.

---

### File Interaction

Once connected to an SMB share, files can be downloaded directly.

- **Command used to download files:** `get`

This allows retrieval of files from the remote system for offline analysis.

---

## Exploitation

### Remote Command Execution

After gaining sufficient access through SMB, an interactive shell is obtained using an Impacket tool.

- **Impacket tool used:** `psexec.py`
- **Result:** Interactive shell on the target system

This method leverages SMB credentials and Windows service creation to execute commands remotely.

---

## Key Concepts Learned

- Bypassing ICMP-based host discovery
- Understanding SMB architecture and administrative shares
- Enumerating and interacting with SMB services
- Downloading files from remote SMB shares
- Gaining remote shells using Impacket tooling

---

## Final Status

- **User access:** Achieved  
- **Root/System access:** Achieved  
- **Root flag:** Owned ✅

---

## Notes

This lab demonstrates how misconfigured or exposed SMB services can lead directly to full system compromise.  
Proper firewall configuration, restricted administrative shares, and credential hygiene are critical for securing Windows environments.

---

## Author

**Developed by**  
Gresa Hisa (@gresium) — AI & Cybersecurity Engineer | AI & Machine Learning Specialist  
GitHub: https://github.com/gresium
