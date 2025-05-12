# 🛡️ Vulnerability Assessment: Advanced Nmap Scan

## 🔍 Objective
The goal of this vulnerability assessment is to perform an in-depth network scan using Nmap on four target IPs (172.16.151.187–190) within a controlled Kali Linux environment. The scan will identify open ports, services running on those ports, potential vulnerabilities, and areas requiring security improvements. The findings will be analyzed, and actionable recommendations will be provided to mitigate risks, tailored specifically for a technical shift supervisor responsible for system security management.

## 🧰 Tools Used
- Nmap
- Kali Linux Terminal
- VIrusTotal

## 🧠 Skills Gained
- Mastery of advanced Nmap scanning techniques, including SYN scans and version detection.
- Service and OS fingerprinting to identify the specific version of software running on target systems.
- Analyzing network scan results to determine potential vulnerabilities and security risks.
- Risk assessment and prioritization to identify critical vulnerabilities that require immediate action.
- Providing clear, actionable recommendations to mitigate security risks for system administrators.

---

## 📄 Full Report

<details>
<summary>Click here to view the full scan report</summary>

### 🔎 Scan Summary

#### **Target: 172.16.151.187**  
- **Open Ports:**  
  - 22 (SSH)  
  - 80 (HTTP)

- **Services Identified:**  
  - **SSH:** SSH-2.0-OpenSSH_7.4  
  - **HTTP:** Apache HTTPD 2.4.6 (CentOS)

**So What?**  
- **SSH (OpenSSH 7.4)**: This version is outdated and contains vulnerabilities such as **CVE-2018-15473**, a user enumeration issue, and **CVE-2017-15906**, which allows attackers to bypass authentication. SSH is a high-priority attack vector, especially when exposed to the internet without proper access restrictions.
- **Apache HTTPD 2.4.6**: This version of Apache has known vulnerabilities, including **CVE-2017-3169**, a denial of service issue, and **CVE-2014-0231**, a buffer overflow vulnerability. Apache is commonly targeted by attackers to gain unauthorized access.

**Recommendations:**  
- **SSH**: Update OpenSSH to the latest stable version (currently OpenSSH 8.0).  
- Restrict SSH access by using firewall rules to only allow specific IPs.  
- Implement **Fail2ban** or similar tools to protect against brute-force login attempts.  
- **Apache HTTPD**: Update Apache to the latest stable version (currently 2.4.51).  
- Use a Web Application Firewall (WAF) to block known attacks targeting Apache.

---

#### **Target: 172.16.151.188**  
- **Open Ports:**  
  - 445 (SMB)  
  - 139 (NetBIOS)  
  - 135 (RPC)

- **Services Identified:**  
  - **SMB:** Microsoft Windows SMB  
  - **NetBIOS & RPC:** Remote management services

**So What?**  
- **SMB (Port 445)**: The presence of SMB without proper security configurations (e.g., signing) increases the risk of exploitation using techniques such as **EternalBlue** (**CVE-2017-0144**), which can allow attackers to execute arbitrary code remotely.
- **NetBIOS (Port 139) and RPC (Port 135)**: These are legacy protocols that are often targeted for lateral movement in a network. In combination, they provide remote management and file-sharing capabilities that can be exploited by attackers for unauthorized access.

**Recommendations:**  
- **SMB**: Enforce **SMB signing** to protect against man-in-the-middle attacks.  
- Disable **SMBv1** and ensure that only **SMBv2/SMBv3** are enabled.  
- Patch all systems to ensure they are not vulnerable to SMB exploits like **EternalBlue**.  
- **NetBIOS & RPC**: Disable or restrict these services to internal networks only.  
- Implement network segmentation to isolate critical systems from less secure zones.

---

#### **Target: 172.16.151.189**  
- **Open Ports:**  
  - 21 (FTP)  
  - 23 (Telnet)  
  - 80 (HTTP)

- **Services Identified:**  
  - **FTP:** vsFTPd 2.3.4  
  - **Telnet**: Default Telnet service  
  - **HTTP:** Apache HTTP Server

**So What?**  
- **FTP (vsFTPd 2.3.4)**: Known for the **CVE-2011-2523** backdoor vulnerability, which allows remote attackers to execute arbitrary code on affected systems. FTP is an unencrypted protocol that transmits sensitive information, including login credentials, in plaintext.
- **Telnet**: An inherently insecure protocol that sends data, including login credentials, in plaintext. It is considered obsolete and should never be used for remote management.

**Recommendations:**  
- **FTP**: Disable FTP and replace it with **SFTP** (SSH File Transfer Protocol), which offers secure, encrypted communication.  
- **Telnet**: Disable Telnet and use **SSH** for encrypted remote access.  
- If FTP is absolutely necessary, consider using **FTPS** (FTP Secure) or restrict FTP usage to internal networks only.

---

#### **Target: 172.16.151.190**  
- **Open Ports:**  
  - 3306 (MySQL)  
  - 8080 (Tomcat)

- **Services Identified:**  
  - **MySQL**: MySQL Database Server  
  - **Tomcat**: Apache Tomcat 7.0.54

**So What?**  
- **MySQL (Port 3306)**: Exposing a MySQL database to the public internet increases the risk of **brute-force** and **SQL injection** attacks. If the database is misconfigured, attackers may exploit these weaknesses.
- **Tomcat (Port 8080)**: **Apache Tomcat 7.0.54** is susceptible to remote code execution vulnerabilities, including **CVE-2017-12617**, which allows attackers to deploy malicious WAR files on the server. If default credentials are not changed, the server can be easily compromised.

**Recommendations:**  
- **MySQL**: Restrict access to MySQL to trusted IP addresses or internal networks.  
- **Tomcat**: Update Tomcat to the latest stable version (currently 9.0.x).  
- Audit Tomcat configurations and ensure the **Manager App** and **Host Manager** are properly secured.  
- **MySQL**: Use strong passwords, enable SSL encryption for database connections, and consider moving the MySQL service behind a VPN.

---

### 🔁 Summary of Risks and Mitigations

| IP Address        | High-Risk Services       | Recommendation Summary                               |
|-------------------|--------------------------|------------------------------------------------------|
| 172.16.151.187    | Outdated SSH/Apache      | Patch SSH and Apache, restrict access, deploy IPS tools |
| 172.16.151.188    | SMB (445), NetBIOS       | Enforce SMB signing, disable SMBv1, patch OS         |
| 172.16.151.189    | FTP, Telnet              | Replace with secure alternatives (SSH/SFTP)          |
| 172.16.151.190    | Tomcat, MySQL            | Restrict access, update services, enforce firewall   |

</details>
