# 🛡️ Vulnerability Assessment: Zenmap Network Scan

## 🔍 Objective
To identify and assess system vulnerabilities using Zenmap and analyze the network security risks associated with various open ports and services.

## 🧰 Tools Used
- Zenmap (Nmap GUI)
- Linux and Windows-based targets

## 🧠 Skills Gained
- Network vulnerability scanning and analysis
- Identification of open ports and services
- Understanding of common network service vulnerabilities (FTP, Telnet, RDP, SSH)
- Risk assessment and mitigation planning for open ports
- Comparison of Linux and Windows-based vulnerabilities

---

## 📄 Full Report

<details>
<summary>Click to expand report</summary>

### 🔎 Vulnerability Scan Analysis

**Target 171.16.11.121:**  
- **Open Ports:**  
  - FTP (21), SSH (22), Telnet (23), HTTP (80), MySQL (3306), SMB (139, 445)  
- **Key Vulnerabilities:**  
  - **High Severity:** FTP and Telnet (unencrypted communication, vulnerable to brute-force attacks)  
  - **Medium Severity:** MySQL open without proper authentication (potential unauthorized access)  
  - **Low Severity:** Apache HTTP server (should be updated and secured)  

**Recommendations:**  
- Disable FTP and Telnet; replace with secure protocols (SFTP, SSH)  
- Restrict MySQL to trusted IPs and require strong authentication  
- Close SMB ports (139, 445) if not necessary, or patch if used  
- Ensure HTTP server is updated and HTTPS is enabled for encryption  

---

**Target 172.16.151.237:**  
- **Open Ports:**  
  - RDP (3389)  
- **Key Vulnerabilities:**  
  - **High Severity:** RDP (exposed to brute-force and man-in-the-middle attacks)  
- **Medium Severity:** Outdated Windows XP (if applicable)  
- **Low Severity:** Weak configuration for RDP access  

**Recommendations:**  
- Restrict RDP access to trusted IPs  
- Implement multi-factor authentication (MFA) for RDP  
- Upgrade the system if it runs Windows XP  

---

**Target 172.16.151.238:**  
- **Open Ports:**  
  - FTP (21), Telnet (23), RDP (3389), HTTP (8080)  
- **Key Vulnerabilities:**  
  - **High Severity:** FTP and Telnet (unencrypted data transmission)  
  - **Medium Severity:** RDP (exposed to brute-force attacks)  
  - **Low Severity:** Apache HTTP server running on CentOS (needs updates)  

**Recommendations:**  
- Disable FTP and Telnet, use secure alternatives (SFTP, SSH)  
- Restrict RDP to trusted IPs, implement MFA  
- Update Apache HTTP server and enable HTTPS for secure communication  

---

**Target 172.16.151.239:**  
- **Open Ports:**  
  - SSH (22), RDP (3389)  
- **Key Vulnerabilities:**  
  - **High Severity:** SSH (weak credentials could lead to brute-force attacks)  
  - **Medium Severity:** RDP (weak configuration could expose system)  
- **Low Severity:** Potential security misconfiguration  

**Recommendations:**  
- Disable root login for SSH, use SSH keys for authentication  
- Restrict RDP to trusted IPs and use MFA  
- Consider VPN for secure remote access  

---

**Target 172.16.151.240:**  
- **Open Ports:**  
  - MSRPC (135), SMB (139, 445), dynamic ports (49152-49157)  
- **Key Vulnerabilities:**  
  - **High Severity:** SMB (if unpatched, susceptible to EternalBlue and other exploits)  
  - **Medium Severity:** MSRPC (vulnerable to remote execution attacks)  
  - **Low Severity:** Outdated operating system (no longer receiving security updates)  

**Recommendations:**  
- Upgrade or patch outdated systems  
- Restrict SMB and MSRPC ports using firewalls  
- Disable SMBv1 if in use and switch to a more secure version  
- Segment network to isolate vulnerable systems  

---

**Target 172.16.151.241:**  
- **Open Ports:**  
  - DNS (53), HTTP (80), MSRPC (135)  
- **Key Vulnerabilities:**  
  - **High Severity:** MSRPC (exposed to potential remote attacks)  
  - **Medium Severity:** IIS web server (could be misconfigured or vulnerable to attacks)  
  - **Low Severity:** DNS server (could be vulnerable to DDoS)  

**Recommendations:**  
- Secure DNS configurations and disable unnecessary recursion  
- Regularly patch IIS web server and strengthen security  
- Restrict MSRPC to internal use and monitor for unusual activity  

---

### 🔁 Nmap vs Zenmap Comparison

- **Zenmap:** Ideal for detailed graphical output and scan management. Useful for repeated scans and creating customized profiles.  
- **Nmap:** Best for command-line scans, scripting, and raw output parsing.  
- **Summary:** Zenmap is great for visual scan analysis and reporting, while Nmap is preferred for automation and advanced scripting. Both tools complement each other for a more comprehensive security assessment.

</details>
