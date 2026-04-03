<div align="center">

# 🖥️ Linux vs Windows Servers

## A Comparative Guide for Security Operations

![Project Status](https://img.shields.io/badge/Status-Completed-brightgreen)
![Platform](https://img.shields.io/badge/Platform-Linux%20%7C%20Windows-blue)
![SOC](https://img.shields.io/badge/SOC-Security%20Operations-red)

**A comprehensive comparison of Linux and Windows servers from a SOC analyst's perspective**

</div>

---

## 📌 What is this project?

This guide provides a **security-focused comparison** between Linux and Windows servers, covering common server roles, attack surfaces, logging locations, and investigation approaches for both platforms.

**But here's what makes it different:**  
It focuses on what SOC analysts actually need — where logs live, how authentication works, and which commands to use when investigating alerts on either platform.

---

## 🎯 Why SOC Analysts Need Both

| Without Both Platforms | With Both Platforms |
|-----------------------|---------------------|
| ❌ Can't investigate Linux alerts if you only know Windows | ✅ Investigate alerts across the entire environment |
| ❌ Miss RDP attack context if you only know Linux | ✅ Recognize attack patterns specific to each OS |
| ❌ Can't communicate with both admin teams | ✅ Communicate effectively with Linux and Windows admins |

---

## 📊 Quick Comparison

| Category | 🐧 Linux Server | 🪟 Windows Server |
|----------|--------------|----------------|
| **Common Roles** | Web, Database, DNS, Mail, Containers | Active Directory, IIS, SQL, Exchange, File Server |
| **Log Location** | `/var/log/` | Event Viewer, `C:\Windows\Logs` |
| **Authentication** | `/etc/passwd`, `/etc/shadow`, PAM | Active Directory, SAM |
| **Security Tools** | SELinux, AppArmor, iptables | Windows Defender, Firewall, AppLocker |
| **Default Ports** | 22 (SSH), 80/443 | 3389 (RDP), 445 (SMB) |

---

## 🔍 What You'll Learn

- 📍 **Where logs live** on each platform
- 🔐 **How authentication events** differ between Linux and Windows
- ⚙️ **Investigation commands** for both operating systems (side-by-side)
- 🕵️ **Real-world investigation scenarios** (Web compromise, brute-force, malware)
- 🎯 **Critical services** every SOC analyst must understand (Active Directory, SMB, RDP)

---

## 🛠️ Commands Covered

| Task | Linux | Windows PowerShell |
|------|-------|-------------------|
| List processes | `ps aux` | `Get-Process` |
| Failed logins | `grep "Failed" /var/log/auth.log` | `Get-WinEvent -ID 4625` |
| Successful logins | `grep "Accepted" /var/log/auth.log` | `Get-WinEvent -ID 4624` |
| Open ports | `ss -tuln` | `Get-NetTCPConnection` |
| Recent files | `find / -mtime -1` | `Get-ChildItem -Recurse` |

---

## 📂 Full Documentation

👉 [Click here for the complete Linux vs Windows Servers Guide](./Linux-vs-Windows-Servers-Guide.md)

---

## ✅ Skills Demonstrated

- Cross-platform security analysis
- Log analysis and correlation
- Authentication event investigation
- Process and persistence detection
- Technical documentation for SOC operations

---

## 💡 Key Takeaway

> *"The methodology stays the same — only the commands change."*

Platform-agnostic proficiency is not a specialization — it is a necessity for SOC analysts.

---

*Prepared by: Yuri Montano | Date: April 2026*
