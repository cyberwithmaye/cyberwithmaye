# Using Multiple Vulnerability Scanners

## Objective
The objective of this assignment was to assess and compare the performance of two widely used vulnerability scanners—**Nessus Essentials** and **Greenbone OpenVAS**—by running scans against a designated target system. The goal was to evaluate differences in the vulnerabilities detected, the quality of reporting, exploitability insights, and remediation guidance.

## Tools Used
- Nessus
- OpenVAS

## Skills Gained
- Experience configuring and running authenticated scans in Nessus and OpenVAS.
- Ability to interpret and compare vulnerability reports across platforms.
- Understanding of common vulnerability metrics (e.g., CVSS, VPR, EPSS).
- Analysis of exploitability and severity ratings.
- Critical thinking in selecting appropriate security tools for an organization’s size and needs.

## 📄 Full Report

<details>
<summary>Click to expand report</summary>

### Comparison Between Nessus and OpenVAS

Vulnerability scanning is important because it helps find weaknesses in systems before attackers do. Nessus Essentials and Greenbone OpenVAS are two of the most used tools for this task, and comparing them helps determine which one provides more useful results.

### Difference Between the Results

After running scans on the target system `172.16.121.154`, I observed several differences in detection and reporting styles. Nessus Essentials detected **46 vulnerabilities** in total: 10 critical, 13 high, 16 medium, and 7 low. OpenVAS found **22 vulnerabilities**: 7 high, 12 medium, and 3 low.

Notably, OpenVAS identified broader system-level risks like:
- The OS reaching **End-of-Life (EOL)**
- Active brute-force attempts on **SSH** and **FTP** services

Nessus, however, identified more **specific software vulnerabilities** and configuration issues, such as:
- Vulnerabilities in **PHP versions** (e.g., GHOST, BACKRONYM)
- Weak **SSH algorithms**
- Multiple **Drupal-related vulnerabilities** with extensive plugin documentation

Nessus provided deeper plugin-based detail, while OpenVAS focused more on web app exposure and general configuration flaws. 

### Vulnerability Comparison – ProFTPD mod_copy

Both tools detected the **ProFTPD mod_copy** vulnerability, which allows an attacker to copy files on the FTP server using `SITE CPFR` and `SITE CPTO` commands. This can be abused for unauthorized access or remote code execution.

**OpenVAS Report**:
- Confirmed vulnerability presence
- Provided a brief description and a general fix recommendation
- Lacked testing data or scoring metrics

**Nessus Report**:
- Provided **exploit metrics**: VPR and EPSS scores
- Included an actual **proof-of-concept test**, showing command output
- Listed exploit tools like **Metasploit** and **Canvas**
- Provided a **detailed fix**, references, and bug report links

Nessus clearly provided more useful and detailed information, making it easier to understand the risk and fix it quickly.

### Best Choice for a Small Organization

For a small organization with under 15 networked devices, I would recommend **Nessus Essentials** for the following reasons:

- Simple and fast setup process
- Better reporting quality and vulnerability prioritization
- Clear remediation advice and exploitability ratings
- Frequent plugin updates via Tenable’s vulnerability database
- Free for scanning up to 16 IP addresses

While OpenVAS is powerful and open-source, it can be slower, more complex to configure, and lacks some of the actionable detail that Nessus provides out-of-the-box. Therefore, Nessus Essentials is more practical for small teams or individual analysts who need efficiency and accuracy in vulnerability management.

</details>
