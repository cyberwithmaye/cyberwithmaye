# 🛡️ Vulnerability Assessment: Advanced Nmap Scan

## 🔍 Objective
The goal of this vulnerability assessment is to perform an in-depth network scan using Nmap on four target IPs (172.16.151.187–190) within a controlled Kali Linux environment. The scan will identify open ports, services running on those ports, potential vulnerabilities, and areas requiring security improvements. The findings will be analyzed, and actionable recommendations will be provided to mitigate risks, tailored specifically for a technical shift supervisor responsible for system security management.

## 🧰 Tools Used
- Nmap
- Kali Linux Terminal
- VIrusTotal

## 🧠 Skills Gained
- Mastery of advanced Nmap scanning techniques, including SYN scans, version detection, and scripts.
- Service and OS fingerprinting to identify the specific version of software running on target systems.
- Analyzing network scan results to determine potential vulnerabilities and security risks.
- Risk assessment and prioritization to identify critical vulnerabilities that require immediate action.
- Providing clear, actionable recommendations to mitigate security risks for system administrators.

---

## 📄 Full Report

<details>
<summary>Click here to view the full scan report</summary>

## 🔍 Target: `172.16.151.187`

### Open Ports & Services:
- **TCP 2222**: OpenSSH 9.2p1  
- **TCP 4000**: Apache httpd 2.4.57  
- **UDP 631**: IPP (CUPS)  
- **UDP 5353**: mDNS/Zeroconf

### Key Vulnerabilities:
- **CVE-2023-31122** – Apache `mod_macro` out-of-bounds read
- **CVE-2024-47176** – CUPS remote execution via IPP
- **mDNS** – Exposes system to MITM and service enumeration attacks

### Recommendations:
- Restrict SSH to trusted IPs and enforce key-based auth
- Patch Apache to latest version; disable directory listing
- Disable IPP and mDNS if not required; block externally with firewall
- Perform regular vulnerability assessments

---

## 🔍 Target: `172.16.151.188`

### Open Ports & Services:
- **TCP 2345**: Telnet (Linux/MikroTik/OpenWrt)

### Key Risks:
- Telnet sends data in plaintext  
- Easily exploited for credential theft and MITM

### Recommendations:
- Disable Telnet entirely  
- Use SSH with encrypted key-based authentication  

---

## 🔍 Target: `172.16.151.189`

### Open TCP Ports:
- **135** MSRPC  
- **389** LDAP  
- **88** Kerberos  
- **139, 445** SMB/NetBIOS  
- **3389** RDP  
- **80, 8530, 8531** Microsoft IIS (TRACE enabled)

### Open UDP Ports:
- **53** DNS  
- **67, 68** DHCP  
- **88** Kerberos  
- **123** NTP  
- **137, 138** NetBIOS  
- **500, 4500** ISAKMP/NAT-T

### Key Vulnerabilities:
- XST via HTTP TRACE (leads to session hijacking)  
- SMB/MSRPC increase risk of remote code execution  
- RDP can be attacked via BlueKeep (CVE-2019-0708)  
- NTP & NetBIOS expose system to DoS and information leaks

### Recommendations:
- Disable TRACE and enforce HTTPS on web servers  
- Disable unnecessary SMB/NetBIOS ports  
- Restrict RDP access, use MFA + VPN  
- Use strong encryption and regular patching  

---

## 🔍 Target: `172.16.151.190`

### Open Ports:
- **80** HTTP (IIS 10.0, TRACE enabled)  
- **135** MSRPC  
- **445** SMB (signing disabled)  
- **3389** RDP (self-signed cert)  
- **8443** HTTPS

### Critical Vulnerabilities:
- **CVE-2017-0143 (MS17-010 / EternalBlue)** – Remote code execution via SMBv1  
- **TRACE method on HTTP** – Cross-Site Tracing  
- **SMB Signing Disabled** – Enables MITM and spoofing  
- **RDP with Self-Signed Cert** – Susceptible to MITM attacks

### Recommendations:
- Apply MS17-010 patch or disable SMBv1  
- Enable SMB signing  
- Use trusted SSL certs for RDP, restrict access  
- Disable TRACE method and use HTTPS  
- Upgrade unsupported Windows systems  

---

## ✅ Final Recommendations

- Perform regular **vulnerability scans** and **patch management**
- Disable or block unused services via **firewall rules**
- Enforce **multi-factor authentication** and **key-based login**
- Use **network segmentation** for critical services
- Monitor **logs and unusual activity**

---
</details>
