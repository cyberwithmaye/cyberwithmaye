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

**Scan Results**:
- **Nessus Essentials** identified **46 vulnerabilities**:
  - 10 Critical
  - 13 High
  - 16 Medium
  - 7 Low
- **OpenVAS** identified **22 vulnerabilities**:
  - 7 High
  - 12 Medium
  - 3 Low

The most noticeable difference between the tools was in the depth and breadth of vulnerability detection. Nessus provided significantly more comprehensive coverage of software-specific issues, while OpenVAS focused more on broader system-level risks such as:
- End-of-life operating system detection
- SSH and FTP brute-force detection
- Exposed web app installers and file disclosures

Nessus, on the other hand, highlighted:
- Deprecated or vulnerable PHP versions (e.g., GHOST, BACKRONYM)
- Weak SSH algorithm configurations
- Multiple issues with web services like Drupal, offering detailed plugin output and remediation guidance

### Vulnerability Comparison: ProFTPD mod_copy

Both scanners detected the **ProFTPD mod_copy** vulnerability, which allows attackers to use the `SITE CPFR` and `SITE CPTO` commands to copy files on an FTP server. This can lead to **unauthorized file access** or even **remote code execution**.

**Comparison of Scanner Reports**:
- **Nessus Essentials**:
  - Provided a detailed explanation of the vulnerability
  - Included **Vulnerability Priority Rating (VPR)** and **Exploit Prediction Scoring System (EPSS)**
  - Showed **live test output** using CPFR to confirm the vulnerability
  - Referenced **attack tools** like Metasploit and Canvas
  - Offered specific remediation steps and a link to the official bug tracker

- **OpenVAS**:
  - Confirmed vulnerability presence
  - Provided a short description and general mitigation advice
  - Offered fewer contextual details, lacking exploit examples or scoring metrics

**Conclusion**: Nessus Essentials delivered more **actionable, detailed, and validated information**, making it far superior for vulnerability management and remediation planning.

### Recommendation for Small Organizations

For organizations with fewer than 15 networked devices, I strongly recommend using **Nessus Essentials** as the primary vulnerability scanner:

- **Benefits**:
  - Detailed and prioritized vulnerability reporting
  - Regular plugin updates via Tenable
  - Fast scan times compared to OpenVAS
  - Intuitive interface and low learning curve
  - Free version supports up to **16 IP addresses**

While OpenVAS is open-source and powerful in larger or more customized environments, it requires more time for configuration and deeper familiarity with vulnerability scanning concepts. Nessus Essentials offers better **out-of-the-box value** for small IT teams focused on quick insights and secure configurations.

</details>
