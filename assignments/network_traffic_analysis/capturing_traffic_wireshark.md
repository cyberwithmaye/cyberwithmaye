# Capturing & Analyzing a Potential Network Incident

## Objective
The objective of this analysis was to investigate suspicious network traffic involving two IP addresses on the organization's internal network using Wireshark. As a junior Cybersecurity Analyst, I was tasked with identifying types of network scans, assessing potential threats, and recommending appropriate mitigation strategies.

## Tools Used
- **Wireshark** – for capturing and analyzing packet-level network traffic    

## Skills Gained
- Applied multiple advanced **Wireshark display filters** to detect scan types  
- Gained hands-on experience in identifying and differentiating between various **TCP port scanning techniques** (SYN, Connect, Null, FIN, Xmass)  
- Interpreted **FTP login attempts** and understood brute-force indicators  
- Analyzed **SSH handshake and key exchange protocols**  
- Developed the ability to **formulate mitigation strategies** based on network forensic evidence  
- Improved report-writing skills for **technical security documentation**

---

## 📄 Full Report

<details>
<summary>Click to expand report</summary>

## Incident Analysis Report

This report analyzes a potential cybersecurity incident involving suspicious network traffic between two IP addresses within the internal network: **172.16.151.113** (target system) and **172.16.151.128** (potential attacker). The investigation was performed using Wireshark and focused on identifying scanning behavior, login attempts, and service enumeration.

### Executive Summary

A host on the internal network (172.16.151.128) appears to have conducted multiple types of reconnaissance scans against another internal system (172.16.151.113), likely in preparation for a targeted attack. The captured packets reveal the use of various TCP scan types, followed by failed FTP login attempts and an attempted SSH connection. The pattern of behavior suggests a methodical intrusion attempt, beginning with service discovery and culminating in brute-force authentication attempts.

---

### Detailed Findings

#### 1. TCP SYN Scan  
- **Filter Applied**: `tcp.flags.syn==1 and tcp.flags.ack==0 and tcp.window_size<=1024`  
- **Purpose**: Commonly used for stealthy port scanning, this method sends SYN packets to probe for open ports. If a SYN-ACK is returned, the port is likely open.
- **Observation**: Multiple SYN packets were directed at a range of ports on 172.16.151.113 from 172.16.151.128, suggesting the attacker was mapping open services without completing the handshake to avoid detection.

#### 2. TCP Connect() Scan  
- **Filter Applied**: `tcp.flags.syn==1 and tcp.flags.ack==0 and tcp.window_size>1024`  
- **Purpose**: This method attempts to complete a full TCP handshake to definitively determine if a port is open.
- **Observation**: The handshake was completed on several ports, indicating live services and confirming the attacker’s intent to verify responsive ports before further exploitation.

#### 3. TCP Null Scan  
- **Filter Applied**: `tcp.flags==0`  
- **Purpose**: Sends packets with no flags set. This scan attempts to exploit how different operating systems respond to unusual packets, often bypassing poorly configured firewalls.
- **Observation**: The attacker sent multiple null-flag packets, signaling a more advanced level of scanning designed to evade detection.

#### 4. TCP FIN Scan  
- **Filter Applied**: `tcp.flags==0x001`  
- **Purpose**: Sends FIN packets without an existing session. Closed ports usually respond with a RST, while open ports ignore it.
- **Observation**: Multiple FIN packets were identified, supporting the hypothesis of an advanced scan for host discovery and firewall evasion.

#### 5. TCP Xmas Scan  
- **Filter Applied**: `tcp.flags.fin==1 && tcp.flags.push==1 && tcp.flags.urg==1`  
- **Purpose**: Sends a packet with FIN, PSH, and URG flags set. Like Null and FIN scans, it's meant to exploit how different OSes respond to malformed packets.
- **Observation**: The use of Xmas scans indicates the attacker is testing firewall behavior and OS fingerprinting.

---

### FTP Login Attempts

- **Service Detected**: vsFTPd 3.0.5 running on 172.16.151.113  
- **Login Attempts**:
  - Username: `cyb201`  
  - Password: `notyourpassword`  
- **Response**: `530 Login incorrect` (repeated multiple times)  
- **Analysis**: The attacker attempted a brute-force login using guessed credentials. Though the attempts failed, the repeated tries suggest intent to gain unauthorized access to the FTP service. This behavior should be monitored and potentially blocked.

---

### SSH Connection Attempt

- **Service Detected**: OpenSSH 8.2p1 on Ubuntu  
- **Session Details**:
  - Successful key exchange using Elliptic Curve Diffie-Hellman (ECDH)
  - Algorithms involved: curve25519-sha256, aes128-ctr, hmac-sha2-256  
- **Analysis**: Although the SSH handshake was completed, there is no evidence of a successful login. This could be a probe to confirm service availability, or the attacker may have been testing for weak keys or attempting to prepare for future brute-force attacks.

---

### Risk Assessment

| Indicator | Severity | Description |
|----------|----------|-------------|
| Port scans | High | Comprehensive scanning using multiple techniques indicates pre-attack reconnaissance. |
| FTP brute-force | Medium | Repeated login attempts with incorrect credentials suggest unauthorized access attempts. |
| SSH probing | Medium | Confirmed service availability; possible staging for future attacks. |

---

### Recommendations

1. **Isolate and block IP address 172.16.151.128** immediately via firewall or VLAN controls to stop ongoing scans and attacks.
2. **Review all authentication logs** on 172.16.151.113 for unusual login activity across FTP, SSH, and RDP.
3. **Disable unused services and ports**, particularly FTP if not required, and restrict SSH to internal admins via key-based authentication only.
4. **Implement intrusion detection/prevention (IDS/IPS)** to detect and alert on port scan behaviors.
5. **Enforce account lockout policies** to prevent brute-force login attempts on FTP and SSH.
6. **Enable logging and alerting** for repeated failed login attempts.
7. **Update service software** to the latest secure versions (e.g., vsFTPd and OpenSSH).
8. **Restrict RDP access** using a VPN or jump host and disallow direct exposure to internal systems.

---

### Conclusion

The packet capture reveals clear evidence of reconnaissance and intrusion activity from an internal host (172.16.151.128). The attacker used a combination of advanced port scanning techniques and brute-force login attempts to probe services on 172.16.151.113. Although no successful compromise was identified, the intent and methodology are consistent with early-stage intrusion tactics. Immediate containment and continued monitoring are essential to prevent future breaches.

</details>
