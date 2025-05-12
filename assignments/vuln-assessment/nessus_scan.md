# 🛡️ Vulnerability Assessment: Nessus Vulnerability Scan

## 🔍 Objective
To identify and assess system vulnerabilities using Nessus Vulnerability Scanner and analyze the differences between Nessus and Nmap scan results.

## 🧰 Tools Used
- Nessus Essentials
- Nmap
- Kali Linux

## 🧠 Skills Gained
- Vulnerability scanning and analysis
- Risk prioritization (high/medium/low)
- CVE research and mitigation planning
- Comparison of active reconnaissance tools
- Understanding of encryption weaknesses and SMB security flaws

---

## 📄 Full Report

<details>
<summary>Click to expand report</summary>

### 🔎 Vulnerability Scan Analysis

**Target 172.16.151.135:**  
- Total of 37 vulnerabilities found  
- **High Severity:** Weak SSL/TLS configurations (self-signed certs, anonymous cipher suites)  
- **Medium Severity:**  
  - RDP MITM vulnerability  
  - CUPS unauthenticated printer registration (CVE-2024-47176)  
  - Deprecated TLS versions (1.0 & 1.1)  
- **Low Severity:** ICMP timestamp disclosure

**Target 172.16.151.136:**  
- Total of 44 vulnerabilities  
- **High Severity:**  
  - SSL Medium Strength Ciphers (SWEET32)  
  - SSL RC4 Cipher (Bar Mitzvah Attack)  
- **Medium Severity:**  
  - SMB Signing Not Required  
  - Self-signed SSL certs and old TLS  
- **Low Severity:** ICMP timestamp disclosure

---

### 🧪 Medium Vulnerability Focus: SMB Signing Not Required

SMB Signing Not Required is a medium-risk vulnerability that allows unauthenticated or manipulated SMB communication. Without SMB signing, attackers can perform MITM attacks to intercept or tamper with file shares.

**How to Fix:**  
Use Group Policy (`gpedit.msc`) > Local Policies > Security Options >  
Enable **"Microsoft network server: Digitally sign communications (always)"**.  
Also use strong authentication/encryption for additional protection.

---

### 🔁 Nmap vs Nessus Comparison

- **Nessus:** Best for vulnerability detection, detailed CVE insights, and remediation tips  
- **Nmap:** Ideal for port discovery, OS detection, and service enumeration  
- **Summary:** Use both together for a more complete security scan. Nmap supports scripting, but lacks Nessus’ detailed vulnerability insight.

</details>
