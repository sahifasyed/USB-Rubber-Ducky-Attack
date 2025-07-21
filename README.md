# USB-Rubber-Ducky-Attack

📝 **Grade Awarded**: 72/100 (Distinction)

A proof-of-concept Human-Interface-Device (HID) attack that escalates privileges on a Windows 10 VM.  
When the Rubber Ducky is inserted, it:

1. Creates a hidden local administrator account  
2. Enables Remote Desktop Protocol (RDP) and opens the firewall port  
3. Adds persistence via a scheduled task  
4. Clears Windows security logs to reduce forensic artifacts  

The full exploit is demonstrated in the accompanying video and documented step-by-step in the deliverables below.

---

## 📹 Demo Video

📁 https://drive.google.com/file/d/1KRpmebxnaKvgBPN0bWiJidG5vSjQHcrr/view?usp=sharing

---

## 🧰 Tactics, Techniques & Procedures (MITRE ATT&CK)

| Tactic                | Technique (ID) | Where Used in Payload |
|-----------------------|----------------|-----------------------|
| Initial Access        | **T1204.002** – Malicious USB Device | Rubber Ducky delivers keystroke payload |
| Privilege Escalation  | **T1136.001** – Create Local Account | Hidden admin account `sys_cache` |
| Defense Evasion       | **T1070.001** – Clear Windows Event Logs | `wevtutil cl` commands |
| Persistence           | **T1053.005** – Scheduled Task        | Task runs PowerShell on logon |
| Lateral Movement      | **T1021.001** – Remote Desktop Protocol | RDP enabled & firewall opened |

---

## 🛡️ Mitigation Strategies

* **USB Control** – Implement HID whitelisting or block untrusted USB devices (e.g., Microsoft Defender USB policy, endpoint agents such as EDR).  
* **Least-Privilege** – Disable automatic admin logon; enforce separate admin credentials and PAM.  
* **Log Forwarding** – Ship logs to a remote, tamper-proof SIEM before local clearing occurs.  
* **Script Blocking** – Constrain PowerShell and VBScript execution with Constrained Language Mode and WDAC.  
* **RDP Hardening** – Require NLA, lock RDP to VPN subnets, monitor for new firewall exceptions.

---
