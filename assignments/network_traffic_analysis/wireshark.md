# 📊 Network Traffic Analysis: Wireshark

## 🔍 Objective
To analyze two Wireshark capture files and investigate network traffic involving ARP, DNS, and HTTP protocols, and to detect suspicious behavior possibly related to a security incident.

## 🧰 Tools Used
- Wireshark

## 🧠 Skills Gained
- Network protocol analysis (ARP, DNS, HTTP, TCP/IP)
- Identifying host communication behavior
- Understanding and interpreting packet-level data
- Detecting signs of suspicious or malicious activity from PCAP data
- Correlating traffic to determine possible causes of compromise

---

## 📄 Full Report

<details>
<summary>Click to expand report</summary>

### 🔎 Network Traffic Analysis

#### 🧪 Part A: Protocol Traffic Analysis (`HO1-PartA.pcapng`)

**🔸 ARP Traffic**
- **Request Frame**: Frame 1  
- **Response Frame**: Frame 2  
- **Requested IP Address**: `192.168.94.2`  
- **Analysis**:  
  The device at `192.168.94.152` initiated an ARP request to communicate with `192.168.94.2`, likely because it did not have the MAC address cached—either it was the first connection or the address had expired from memory.

**🔸 DNS Traffic**
- **Frame Summary**:
  - Frame 3: A record query for `robust.cs.utep.edu` (IPv4)
  - Frame 4: AAAA record query (IPv6)
  - Frame 5: A record response with `129.108.18.226`
  - Frame 6: SOA record for IPv6 query (no IPv6 address returned)
- **Hostname Queried**: `robust.cs.utep.edu`  
- **Resolved IP Address**: `129.108.18.226`  
- **Correlation with ARP**:  
  The DNS result (129.108.18.226) is unrelated to the ARP request (for 192.168.94.2), suggesting they are separate activities.

**🔸 HTTP Traffic**
- **Requested URL**: `http://robust.cs.utep.edu/~freudent/test.html`
- **TCP Handshake Frames**: 7, 8, 9  
- **TCP Teardown Frames**: 14, 15, 16  
- **Server Details**:
  - IP Address: `129.108.18.226`
  - Port: `80`
- **Client Details**:
  - IP Address: `192.168.94.152`
  - Port: `51562`
- **Traffic Details**:
  - HTTP Request: Frame 10 (`GET /~freudent/test.html`)
  - HTTP Headers: Frame 10
  - HTTP Response: Frame 12 (`HTTP/1.1 200 OK (text/html)`)

---

#### 🚨 Part B: Security Incident Investigation (`HO1-PartB.pcapng`)

**Scenario**  
Mike reported his computer as "acting weird." A PCAP file of network activity just before the report was analyzed for anomalies.

**Findings**
- **Timeframe**: February 8, 2015, from 18:20 to 18:44 UTC  
- **Device Info**:
  - Hostname: `Mike-PC`
  - IP: `172.16.137.40`
  - MAC: `08:00:2b:ef:ab:7c`
- **Suspicious Behavior**:
  - Access to questionable websites
  - Communication with potentially malicious IP addresses
  - Heavy presence of TLS/SSL packets, followed by a flood of ACK and RST packets (suggesting tampering or session hijacking)
  - LLMNR and NetBIOS name queries potentially leaking system information
  - STUN and SSDP traffic, which may indicate covert communication channels

**Conclusion**  
The symptoms suggest a compromise via malware or a man-in-the-middle (MITM) attack. This likely explains the abnormal behavior Mike observed.

</details>
