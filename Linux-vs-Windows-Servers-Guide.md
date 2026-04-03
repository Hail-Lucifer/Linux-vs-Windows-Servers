<div align="center">

# 🖥️ Linux vs Windows Servers

## A Comparative Guide for Security Operations

![Project Status](https://img.shields.io/badge/Status-Completed-brightgreen?style=for-the-badge)
![Platform](https://img.shields.io/badge/Platform-Linux%20%7C%20Windows-blue?style=for-the-badge)
![SOC](https://img.shields.io/badge/SOC-Security%20Operations-red?style=for-the-badge&logo=security)
![Analyst](https://img.shields.io/badge/Role-SOC%20Analyst-purple?style=for-the-badge)

![Commands](https://img.shields.io/badge/Includes-Investigation%20Commands-green?style=flat-square)
![Logs](https://img.shields.io/badge/Focus-Log%20Analysis-orange?style=flat-square)
![Authentication](https://img.shields.io/badge/Focus-Authentication%20Events-yellow?style=flat-square)
![Incident Response](https://img.shields.io/badge/Focus-Incident%20Response-red?style=flat-square)

**Prepared by:** Yuri Montano  
**📅 Date:** April 2026

</div>


<img width="910" height="391" alt="image" src="https://github.com/user-attachments/assets/57d41a21-748d-45b6-9e6f-4f0fc09235e2" />




---

## 📋 Table of Contents

| Section | Page |
|---------|------|
| 1. Introduction 
| 2. Why SOC Analysts Need Both Linux and Windows Knowledge 
| 3. Linux Server Overview 
| 4. Windows Server Overview 
| 5. Side-by-Side Comparison 
| 6. Critical Windows Server Services for SOC Analysts 
| 7. Investigation Commands Comparison 
| 8. Real-World Investigation Scenarios 
| 9. Key Takeaways for SOC Analysts 
| 10. Conclusion 

---

## 1. 📖 Introduction

In any **Security Operations Center (SOC)**, understanding the infrastructure you are protecting is essential. Alerts do not come with labels like "this is a Linux server" or "this is a Windows server" — the analyst must recognize the environment based on logs, processes, and behavior.

This document provides a comprehensive comparison between 🐧 **Linux** and 🪟 **Windows** servers from a security analyst's perspective. It covers:

- 🔧 Common server roles
- 🖥️ Operating system differences relevant to investigations
- 🎯 Attack surfaces
- 🔍 Investigation approaches for both platforms

The goal is to equip **SOC analysts** with the knowledge needed to investigate alerts effectively, regardless of the underlying operating system.

---

## 2. 🎯 Why SOC Analysts Need Both Linux and Windows Knowledge

Most organizations run a **mix of both operating systems**:

| Platform | Common Uses |
|----------|-------------|
| 🐧 **Linux Servers** | Web servers, databases, DNS, email, development environments |
| 🪟 **Windows Servers** | Active Directory, file sharing, Exchange, legacy applications |

### ⚠️ The Problem

Without proficiency in both platforms, analysts face significant limitations:

- ❌ When an alert shows suspicious processes on a Linux server, an analyst who only knows Windows cannot investigate properly
- ❌ When a brute-force attack targets RDP on a Windows server, an analyst who only knows Linux misses the context

### ✅ The Solution

Analysts who understand **both platforms** can:

- 🔍 Investigate alerts across the entire environment
- 🎯 Recognize attack patterns specific to each operating system
- 💬 Communicate effectively with both Linux and Windows administrators

---

## 3. 🐧 Linux Server Overview

### 3.1 Common Linux Distributions

| Distribution | Description | Common Use Cases |
|--------------|-------------|------------------|
| 🟠 **Ubuntu Server** | Most common for web servers and cloud environments | Web servers, cloud deployments (AWS, Azure, GCP) |
| 🔵 **Debian** | Known for stability, foundation for Ubuntu | Production environments prioritizing reliability |
| 🔴 **Red Hat Enterprise Linux (RHEL)** | Enterprise standard with paid support | Government, financial sectors, compliance-heavy environments |
| 🟡 **CentOS / Rocky Linux** | Free alternatives to RHEL | Web hosting, academic institutions |
| 🟢 **Alpine Linux** | Extremely lightweight, minimal attack surface | Containers, Docker images |

### 3.2 Common Linux Server Roles

| Role | Description | Log Location |
|------|-------------|--------------|
| 🌐 **Web Server (Apache/Nginx)** | Hosts websites and web applications | `/var/log/apache2/` or `/var/log/nginx/` |
| 🗄️ **Database Server (MySQL/PostgreSQL)** | Stores structured data for applications | `/var/log/mysql/` or `/var/log/postgresql/` |
| 📧 **DNS Server (BIND)** | Resolves domain names to IP addresses | `/var/log/named/` |
| 📨 **Mail Server (Postfix/Dovecot)** | Handles email sending and receiving | `/var/log/mail.log` |
| 📁 **File Server (NFS/Samba)** | Shares files across the network | `/var/log/` |
| 🐳 **Container Host (Docker)** | Runs containerized applications | `/var/log/docker/` |

### 3.3 🔒 Security Strengths of Linux

| Strength | Description |
|----------|-------------|
| 🔓 **Open Source** | Source code publicly available for auditing; vulnerabilities found and fixed quickly |
| 🔐 **Granular Permissions** | Fine-grained access control (rwx for owner/group/others) |
| 🛡️ **Mandatory Access Control** | SELinux and AppArmor provide additional security layers |
| 📦 **Centralized Package Management** | GPG-signed packages from verified repositories |
| 📉 **Minimal Installation** | Install only what's needed — reduces attack surface |

### 3.4 ⚠️ Security Weaknesses of Linux

| Weakness | Description |
|----------|-------------|
| 🔧 **Complex Configuration** | Properly securing Linux requires deep expertise |
| 📁 **Fragmented Logging** | Logs scattered across multiple directories |
| 📚 **Steep Learning Curve** | Command-line proficiency required |
| 👑 **Root Privilege Mistakes** | Services running as root create dangerous privilege escalation paths |

---

## 4. 🪟 Windows Server Overview

### 4.1 Common Windows Server Versions

| Version | Description | Use Cases |
|---------|-------------|-----------|
| 🔵 **Windows Server 2019 (WS2019)** | Stable, mature, widely deployed | Legacy applications requiring long-term support |
| 🟣 **Windows Server 2022 (WS2022)** | Enhanced security, Secured-core Server | Organizations adopting modern security practices |
| 🟢 **Windows Server 2025 (WS2025)** | Latest version, cloud integration | AI-enhanced security capabilities |
| ⚙️ **Windows Server Core** | Minimal installation, no GUI | Reduced attack surface deployments |

### 4.2 Common Windows Server Roles

| Role | Description | Ports | SOC Importance |
|------|-------------|-------|----------------|
| 👥 **Active Directory (AD)** | Centralized authentication and policy management | 389 (LDAP), 636 (LDAPS), 88 (Kerberos) | 🔴 **Crown jewel** — compromising AD gives attacker control over everything |
| 🌐 **IIS Web Server** | Hosts .NET web applications and APIs | 80, 443 | Monitor for SQL injection, directory traversal |
| 🗃️ **SQL Server** | Enterprise database platform | 1433 | Business-critical applications |
| 📧 **Exchange Server** | Corporate email and calendar | 25, 443, 587 | On-premises email infrastructure |
| 📁 **File Server (SMB)** | Network file sharing | 445 | ⚠️ Major ransomware vector (WannaCry, NotPetya) |
| 🖥️ **Remote Desktop Services (RDS)** | Graphical remote access | 3389 | 🎯 Frequent brute-force target |

### 4.3 🔒 Security Strengths of Windows

| Strength | Description |
|----------|-------------|
| 🏢 **Centralized Management** | Active Directory + Group Policy for unified configuration |
| 📊 **Comprehensive Event Logging** | Event Viewer with Security, Application, System, PowerShell logs |
| 🛡️ **Windows Defender** | Built-in antivirus, firewall, and EDR capabilities |
| 🔄 **Streamlined Patch Management** | Windows Update and WSUS for enterprise-wide deployment |

### 4.4 ⚠️ Security Weaknesses of Windows

| Weakness | Description |
|----------|-------------|
| 🔄 **Frequent Patch Cycles** | Constant race between defenders and attackers |
| 🚪 **Large Attack Surface** | Many services enabled by default |
| 🌐 **RDP Exposure** | Frequently exposed to internet, targeted by brute-force |
| 📁 **SMB Vulnerabilities** | WannaCry, NotPetya — devastating ransomware outbreaks |
| 📝 **Registry Complexity** | Difficult to audit changes; attackers hide persistence in obscure locations |

---

## 5. 📊 Side-by-Side Comparison

| Category | 🐧 Linux Server | 🪟 Windows Server |
|----------|--------------|----------------|
| **Common Roles** | Web (Apache/Nginx), Database (MySQL/PostgreSQL), DNS, Mail, Container Host | Active Directory, IIS, SQL Server, Exchange, File Server (SMB) |
| **Default Shell** | Bash, Zsh | PowerShell, CMD |
| **Log Location** | `/var/log/` | Event Viewer, `C:\Windows\Logs` |
| **Authentication** | `/etc/passwd`, `/etc/shadow`, PAM, LDAP | Active Directory, SAM |
| **File Permissions** | rwx (read/write/execute) + `chmod` | ACLs (Access Control Lists) |
| **Security Tools** | SELinux, AppArmor, iptables, Fail2ban | Windows Defender, Windows Firewall, AppLocker |
| **Default Ports** | 22 (SSH), 80/443 (HTTP/HTTPS) | 3389 (RDP), 445 (SMB), 5985/5986 (WinRM) |

---

## 6. 🎯 Critical Windows Server Services for SOC Analysts

| Service | Ports | Purpose | What to Monitor |
|---------|-------|---------|-----------------|
| 👥 **Active Directory (AD)** | 389, 636, 88 | Centralized authentication and policy management | Event ID 4720 (account creation), 4672 (privilege escalation), 4769 (suspicious Kerberos) |
| 🌐 **IIS Web Server** | 80, 443 | Hosting websites and web applications | `C:\inetpub\logs\LogFiles` — SQL injection, directory traversal, suspicious POST requests |
| 📁 **File Server (SMB)** | 445 | Network file sharing | Unusual SMB traffic — major ransomware vector (WannaCry, NotPetya) |
| 🖥️ **RDP Server** | 3389 | Remote graphical access | Failed logins (4625) followed by success (4624), unusual geographic locations, multiple sessions from same IP |

---

## 7. 🔍 Investigation Commands Comparison

| Task | 🐧 Linux Command | 🪟 Windows PowerShell Command |
|------|-----------------|------------------------------|
| 📋 List processes | `ps aux` | `Get-Process` |
| 🔍 Find suspicious process | `ps aux \| grep suspicious` | `Get-Process \| Where-Object {$_.ProcessName -like "*suspicious*"}` |
| ❌ Failed logins | `grep "Failed password" /var/log/auth.log` | `Get-WinEvent -FilterHashtable @{LogName='Security'; ID=4625}` |
| ✅ Successful logins | `grep "Accepted" /var/log/auth.log` | `Get-WinEvent -FilterHashtable @{LogName='Security'; ID=4624}` |
| 🆕 New service installed | `grep "Installed" /var/log/syslog` | `Get-WinEvent -FilterHashtable @{LogName='System'; ID=7045}` |
| 🔌 Open ports | `ss -tuln` | `Get-NetTCPConnection` |
| 🌐 Active connections | `ss -tunp` | `Get-NetTCPConnection \| Where-Object {$_.State -eq "Established"}` |
| 📁 Recently modified files | `find / -mtime -1 2>/dev/null` | `Get-ChildItem -Recurse \| Where-Object {$_.LastWriteTime -gt (Get-Date).AddDays(-1)}` |

---

## 8. 🕵️ Real-World Investigation Scenarios

### Scenario 1: 🌐 Web Server Compromise

| Platform | Investigation Steps |
|----------|---------------------|
| 🐧 **Linux (Apache)** | Examine `/var/log/apache2/access.log` for SQL injection patterns → Check for recently uploaded files in `/var/www/` using `find` → Identify source IPs of suspicious requests |
| 🪟 **Windows (IIS)** | Use PowerShell to examine logs in `C:\inetpub\logs\LogFiles` → Find recently modified files with `Get-ChildItem` → Correlate findings with Security Event Logs for authentication events |

### Scenario 2: 🔑 Brute-Force Attack

| Platform | Investigation Steps |
|----------|---------------------|
| 🐧 **Linux (SSH)** | Use `grep "Failed password" /var/log/auth.log` to view failed attempts → Extract source IP addresses → Check for successful logins from the same IPs |
| 🪟 **Windows (RDP)** | Use `Get-WinEvent` to query Security log for Event ID 4625 (failed logons) → Aggregate source IP addresses → Check for Event ID 4624 (successful logons) from the same IPs |

### Scenario 3: 🦠 Malware Investigation

| Platform | Investigation Steps |
|----------|---------------------|
| 🐧 **Linux** | `ps aux \| sort -rn -k3` to identify high-CPU processes → Check persistence in cron jobs with `crontab -l` → Examine network connections with `netstat -anp` |
| 🪟 **Windows** | `Get-Process \| Sort-Object CPU -Descending` to identify high-CPU processes → Check persistence in scheduled tasks with `Get-ScheduledTask` → Examine registry run keys with `Get-ItemProperty` |

---

## 9. 💡 Key Takeaways for SOC Analysts

| Takeaway | Description |
|----------|-------------|
| 🔄 **Cross-Platform Proficiency** | The most effective SOC analysts develop proficiency across both platforms |
| 🐧 **Linux Strengths** | Dominates web hosting, databases, and containers. Investigations center on `/var/log/` and command-line tools |
| 🪟 **Windows Strengths** | Foundational for identity management (AD), file sharing (SMB), and enterprise apps |
| 🔧 **Core Skills Translate** | Knowing where logs live, understanding authentication events, investigating processes, identifying persistence — methodology stays the same, only commands change |
| 🎯 **Platform-Agnostic Necessity** | Not a specialization — it is a necessity for modern SOC analysts |

---

## 10. 🏁 Conclusion

Understanding both 🐧 **Linux** and 🪟 **Windows** servers is **essential** for any SOC analyst. Modern enterprises run both platforms, and attackers move freely between them — a defender who only knows one is only half effective.

### Summary

| Platform | Strengths | Investigation Focus |
|----------|-----------|---------------------|
| 🐧 **Linux** | Transparency, granular control, minimal installations | `/var/log/`, `grep`, `awk`, `ps aux`, `ss` |
| 🪟 **Windows** | Centralized management, comprehensive logging, integrated security | Event Viewer, Event IDs (4624, 4625, 7045), `Get-WinEvent`, `Get-Process` |

### Final Thought

> *"The methodology stays the same — only the commands change."*


By mastering both Linux and Windows, you position yourself to investigate any alert, on any system, wherever the evidence leads.

---


<div align="center">



</div>
