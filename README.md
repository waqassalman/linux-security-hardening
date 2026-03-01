
# 🔐 Linux OS Security Hardening Lab

![Security](https://img.shields.io/badge/Security-Linux_Hardening-red?style=for-the-badge&logo=linux&logoColor=white)
![Tools](https://img.shields.io/badge/Tools-Lynis%20|%20AIDE%20|%20SSH-blue?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen?style=for-the-badge)
![Course](https://img.shields.io/badge/Course-CSAI_5000-orange?style=for-the-badge)

A hands-on Linux Operating System security hardening lab completed as part of **CSAI 5000: Fundamentals of Cybersecurity** at Humber College. This lab covers real-world security configurations, auditing, and privilege escalation analysis on a Kali Linux environment.

---

## 📋 Lab Objectives

- Configure and analyse Linux file permissions (standard, SUID, SGID, ACLs)
- Understand and demonstrate privilege escalation vectors
- Harden SSH configuration against common attack vectors
- Audit system security posture using Lynis
- Analyse authentication and system logs
- Implement file integrity monitoring with AIDE
- Identify and remediate common misconfigurations

---

## 🛠️ Tools & Technologies

| Tool | Purpose |
|---|---|
| **Lynis 3.1.6** | Security auditing and hardening index scoring |
| **AIDE** | File integrity monitoring and change detection |
| **SSH / sshd** | Secure remote access configuration hardening |
| **Kali Linux** | Lab environment (Kernel 6.16.8) |
| **auditd** | System audit logging |
| **fail2ban** | Brute force protection |
| **umask** | Default file permission control |

```
linux-os-security-hardening/
│
├── README.md                          # This file
├── Lab-OS-Security-Hardening.pdf      # Full lab report with findings
├── configs/
│   ├── sshd_config_hardened           # Hardened SSH configuration
│   └── aide.conf                      # AIDE file integrity config
├── scripts/
│   ├── suid_demo.c                    # SUID vulnerability demonstration
│   └── permission_audit.sh            # File permission audit script
└── reports/
    └── lynis-suggestions.txt          # Full Lynis audit output
```

---

## 🔍 Key Findings & Results

### Lynis Hardening Score
| Before Hardening | After Hardening |
|---|---|
| **64 / 100** | Improvements applied |

### Top Security Issues Identified

**1. auditd Not Enabled (ACCT-9628)**
System audit logging was disabled — no forensic trail of privileged actions. Risk: zero visibility into post-compromise attacker activity.

**2. Default umask Too Permissive (AUTH-9328)**
Default umask of 022 creates world-readable files. Hardened to 027 to enforce least privilege on all newly created files.

**3. fail2ban Not Installed (DEB-0880)**
SSH exposed to unlimited brute force attempts. fail2ban installation recommended to auto-ban IPs after repeated failures.

**4. No Password Policy Configured (AUTH-9286)**
No minimum or maximum password age configured in `/etc/login.defs` — accounts could use weak or unchanged passwords indefinitely.

**5. USB Storage Not Disabled (USB-1000)**
USB storage drivers loaded by default — risk of unauthorized data exfiltration or malicious device insertion.

---

## 🔐 Security Concepts Demonstrated

### File Permissions & Special Bits
- Standard Unix permissions (owner/group/others)
- SUID bit — demonstrated privilege escalation via vulnerable SUID binary
- SGID bit — implemented shared group directory for collaborative access
- ACLs — fine-grained per-user permissions beyond standard Unix model
- umask 077 — least privilege default for new file creation

### SSH Hardening
```
PermitRootLogin no
PasswordAuthentication no
PubkeyAuthentication yes
MaxAuthTries 3
Protocol 2
```

### Privilege Escalation Vectors Identified
- Vulnerable SUID binary using `system()` with unsanitized user input
- World-writable directories in root's PATH (PATH hijacking)
- Insecure cron jobs running as root referencing writable scripts
- Unowned files with no valid user or group

---

## 💡 Key Takeaways

1. **Defence in depth** — no single control is sufficient; security requires layers
2. **Least privilege** — umask, file permissions, and sudo must be configured to give minimum required access
3. **Audit everything** — without auditd and centralised logging (SIEM), there is no forensic trail
4. **SUID is dangerous** — every SUID binary is a potential privilege escalation path and must be audited regularly
5. **SSH hardening is non-negotiable** — disabling root login and password auth eliminates an entire class of attacks

---

## 🚀 How to Reproduce This Lab

### Prerequisites
- Kali Linux VM (or any Debian-based system)
- sudo access
- Internet connection for package installation

### Setup
```bash
# Create lab directory
mkdir -p ~/lab5 && cd ~/lab5

# Install required tools
sudo apt update
sudo apt install lynis aide fail2ban -y

# Run Lynis audit
sudo lynis audit system

# View results
sudo grep -E "warning\[\]|suggestion\[\]" /var/log/lynis-report.dat
```

---

## 📚 Course Information

**Course:** CSAI 5000 — Fundamentals of Cybersecurity  
**Institution:** Humber College, Toronto, ON  
**Program:** Postgraduate Certificate — Cybersecurity & AI  
**Lab:** Lab 7 — Operating System Security Hands-On  
**Duration:** 90 minutes  

---

## 👤 Author

**Waqas Salman, MSc**  
Postgraduate Certificate — Cybersecurity & AI | Humber College  
MSc Computer Science | Middlesex University  

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-blue?style=flat&logo=linkedin)](https://linkedin.com/in/waqas-salman)
[![GitHub](https://img.shields.io/badge/GitHub-Follow-black?style=flat&logo=github)](https://github.com/waqassalman)

---

*Completed as part of the Postgraduate Certificate in Cybersecurity & AI — Humber College, Toronto, ON.*# linux-security-hardening
Linux system hardening lab covering file permissions, SSH security, AIDE, Lynis auditing and privilege escalation
