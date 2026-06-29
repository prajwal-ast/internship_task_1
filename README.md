# Task 1 - Local Network Port Scanning using Nmap

## Cyber Security Internship – Task 1

---

# Objective

The objective of this task was to perform network reconnaissance on my local network using Nmap, identify active hosts, discover exposed TCP services, analyze the security implications of open ports, and observe the scanning process using Wireshark.

This exercise demonstrates one of the first phases of penetration testing—**Information Gathering (Reconnaissance)**.

---

# Tools Used

| Tool | Purpose |
|------|---------|
| Nmap 7.95 | Network discovery and TCP SYN port scanning |
| Wireshark | Packet capture and analysis |
| Kali Linux | Penetration Testing Operating System |

---

# Network Information

| Parameter | Value |
|----------|-------|
| Operating System | Kali Linux |
| Interface | eth0 |
| Local IP Address | 10.240.243.93 |
| Network Range | 10.240.243.0/24 |
| Scan Type | TCP SYN Scan |

---

# Scan Command

```bash
sudo nmap -sS 10.240.243.0/24 -oN scan_results.txt
```

### Explanation

- **sudo** – Executes the scan with administrative privileges.
- **nmap** – Network scanning tool.
- **-sS** – Performs a TCP SYN (Half-Open) Scan.
- **10.240.243.0/24** – Scans every host within the local subnet.
- **-oN** – Saves the scan output in normal text format.

---

# Scan Results

## Hosts Discovered

| IP Address | Open Port | Service | Status |
|------------|----------|---------|--------|
| 10.240.243.121 | 3306 | MySQL | Open |
| 10.240.243.168 | 53 | DNS | Open |
| 10.240.243.93 | None | - | All scanned ports closed |

---

# Port Analysis

## Host: 10.240.243.121

### Port 3306 - MySQL

Description:
The MySQL service is the default database service used by many web applications and enterprise software.

Possible Security Risks

- Unauthorized remote database access
- Weak authentication credentials
- Exposure of sensitive data
- SQL Injection risks if connected applications are vulnerable

Recommendations

- Restrict remote database access.
- Use strong authentication.
- Enable firewall rules.
- Keep MySQL updated with security patches.

---

## Host: 10.240.243.168

### Port 53 - DNS

Description:
DNS (Domain Name System) resolves domain names into IP addresses and is a fundamental network service.

Possible Security Risks

- DNS Cache Poisoning
- DNS Amplification Attacks
- Information Disclosure
- Unauthorized Recursive Queries

Recommendations

- Restrict recursive queries.
- Secure DNS configurations.
- Monitor DNS traffic.
- Apply security updates regularly.

---

## Host: 10.240.243.93 (Scanning Machine)

No open TCP ports were detected among the 1000 most common ports scanned.

This indicates that no commonly exposed TCP services were running on the scanning machine during the assessment, reducing the attack surface.

---

# Wireshark Analysis

During the Nmap TCP SYN scan, Wireshark was used to capture the generated network traffic.

The packet capture demonstrated the TCP Three-Way Handshake process used during port scanning.

Observed Packet Flow

```
Kali Linux
      |
      | SYN
      |
Target Host
      |
      | SYN-ACK (Open Port)
      |
Kali Linux
      |
      | RST
```

For open ports:

- SYN packet sent
- SYN-ACK received
- RST sent by Nmap (Half-Open Scan)

For closed ports:

- SYN packet sent
- RST received from target host

This confirms the behavior of an Nmap TCP SYN Scan.

---

# Key Concepts Learned

- Network Reconnaissance
- Host Discovery
- TCP SYN (Half-Open) Scan
- Open Port Identification
- Service Enumeration
- Basic Risk Assessment
- Packet Capture using Wireshark
- TCP Communication Process

---

# Security Observations

- One device exposed a MySQL database service.
- One device exposed a DNS service.
- The scanning machine had no commonly exposed TCP services.
- Open ports increase the attack surface and should only be exposed when necessary.
- Proper firewall configuration and service hardening are essential to reduce security risks.

---

# Outcome

Through this task, I gained practical experience in:

- Performing local network reconnaissance
- Identifying active hosts
- Discovering exposed network services
- Understanding TCP SYN scanning methodology
- Capturing and analyzing packets using Wireshark
- Assessing basic security risks associated with open ports

This exercise strengthened my understanding of the reconnaissance phase of penetration testing and highlighted the importance of minimizing unnecessary network exposure.


---

# Author

**Prajval Raj K**

Cyber Security Engineering Student

ACS College of Engineering

Cyber Security Internship - Task 1

2026
