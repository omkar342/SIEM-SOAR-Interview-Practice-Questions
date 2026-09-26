# 🔐 Basic Cybersecurity & Networking — Interview Q&A
### Tailored for: Deloitte T&T | Cyber: D&R | Consultant I (XSOAR) Role

> These are foundational questions an interviewer may ask to validate your core knowledge before diving into SIEM/SOAR specifics. Your background in security integration engineering (BloodHound Enterprise + Google SecOps, Sentinel, Elastic, CrowdStrike) gives you real context to anchor these answers. Study these alongside your XSOAR playbook knowledge.

---

## 📋 Table of Contents
1. [Networking Fundamentals](#1-networking-fundamentals)
2. [OSI & TCP/IP Model](#2-osi--tcpip-model)
3. [Common Protocols](#3-common-protocols)
4. [Firewalls, IDS/IPS, and Network Security](#4-firewalls-idsips-and-network-security)
5. [Cryptography & PKI](#5-cryptography--pki)
6. [Threat Intelligence & Attack Frameworks](#6-threat-intelligence--attack-frameworks)
7. [Incident Response Lifecycle](#7-incident-response-lifecycle)
8. [Vulnerability Management](#8-vulnerability-management)
9. [Identity & Access Management (IAM)](#9-identity--access-management-iam)
10. [Log Analysis & SIEM Basics](#10-log-analysis--siem-basics)
11. [Endpoint Security](#11-endpoint-security)
12. [Common Attack Types](#12-common-attack-types)

---

## 1. Networking Fundamentals

### Q1. What is the difference between TCP and UDP?

| Feature | TCP | UDP |
|---|---|---|
| Connection | Connection-oriented (3-way handshake) | Connectionless |
| Reliability | Guaranteed delivery, retransmission | No guarantee of delivery |
| Order | Packets arrive in order | No ordering |
| Speed | Slower (overhead) | Faster |
| Use Cases | HTTP, FTP, SSH, SMTP | DNS, DHCP, VoIP, streaming |

**Key point for SOC**: Attackers often use UDP for DNS tunneling or exploit TCP's 3-way handshake in SYN flood attacks.

---

### Q2. What is the difference between a hub, switch, and router?

- **Hub**: Layer 1 device. Broadcasts traffic to all ports. No intelligence. Creates collision domains.
- **Switch**: Layer 2 device. Uses MAC addresses to forward traffic only to the intended port. Creates separate collision domains.
- **Router**: Layer 3 device. Uses IP addresses to route traffic between different networks (subnets). Makes best-path decisions.

---

### Q3. What is the difference between a private IP and a public IP?

- **Private IPs**: Used within internal networks. Not routable on the internet.
  - `10.0.0.0/8`, `172.16.0.0/12`, `192.168.0.0/16`
- **Public IPs**: Assigned by ISPs. Routable on the internet. Unique globally.

**SOC relevance**: Source IPs from private ranges in firewall logs indicate internal traffic. Public IPs can be looked up in threat intel feeds.

---

### Q4. What is NAT (Network Address Translation)?

NAT translates private IP addresses to a public IP address (and vice versa) so internal devices can communicate with the internet. It also provides a layer of obscurity for internal hosts.

- **SNAT (Source NAT)**: Changes source IP (outbound traffic)
- **DNAT (Destination NAT)**: Changes destination IP (inbound traffic / port forwarding)

---

### Q5. What is a subnet mask and CIDR notation?

A subnet mask defines which portion of an IP address is the network part vs the host part.
- Example: `192.168.1.0/24` → `/24` means 24 bits are for the network = `255.255.255.0` = 256 IPs (254 usable)
- `/32` = single host, `/0` = all IPs

**Practical use**: In SIEM rules, you define network segments using CIDR to scope alerts (e.g., alerts only for traffic leaving the `10.10.0.0/16` internal segment).

---

### Q6. What is a VLAN?

A Virtual LAN (VLAN) is a logical segmentation of a network at Layer 2, even if devices are on the same physical switch. VLANs isolate broadcast domains and improve security.

**Security use**: Segmenting sensitive networks (e.g., PCI, HR, OT) into separate VLANs reduces the blast radius of a breach.

---

### Q7. What is DNS and how does it work?

DNS (Domain Name System) translates human-readable domain names (e.g., `google.com`) to IP addresses.

**Resolution flow:**
1. Client checks local cache
2. Queries recursive resolver (ISP/local)
3. Recursive resolver queries root servers → TLD servers (`.com`) → authoritative name server
4. Returns IP to client

**Security relevance**: DNS is commonly abused for:
- **DNS tunneling** (data exfiltration)
- **DNS poisoning/spoofing**
- **C2 communication** (Domain Generation Algorithms - DGA)

---

### Q8. What is ARP and ARP poisoning?

**ARP (Address Resolution Protocol)**: Maps IP addresses to MAC addresses on a local network (Layer 2). When a device wants to communicate, it broadcasts "Who has IP X?" and the owner replies with its MAC.

**ARP Poisoning**: An attacker sends fake ARP replies to associate their MAC with a legitimate IP, enabling Man-in-the-Middle (MitM) attacks.

---

## 2. OSI & TCP/IP Model

### Q9. Explain the OSI model layers with examples.

| Layer | Name | Examples | Security Relevance |
|---|---|---|---|
| 7 | Application | HTTP, DNS, FTP, SMTP | SQL injection, XSS, malware C2 |
| 6 | Presentation | TLS/SSL, encoding | Encryption, certificate inspection |
| 5 | Session | NetBIOS, RPC | Session hijacking |
| 4 | Transport | TCP, UDP | SYN floods, port scanning |
| 3 | Network | IP, ICMP, routing | IP spoofing, routing attacks |
| 2 | Data Link | Ethernet, ARP, MAC | ARP poisoning, MAC spoofing |
| 1 | Physical | Cables, NICs, hubs | Physical tapping |

---

### Q10. What happens during a TCP 3-way handshake?

1. **SYN**: Client sends a SYN packet to the server (wants to connect)
2. **SYN-ACK**: Server acknowledges and sends back SYN-ACK
3. **ACK**: Client sends final ACK. Connection established.

**Attack relevance**: **SYN Flood** — attacker sends thousands of SYN packets but never completes the handshake, exhausting server resources (DoS attack).

---

### Q11. What is the difference between HTTP and HTTPS?

- **HTTP** (port 80): Unencrypted. Data sent in plaintext — vulnerable to interception.
- **HTTPS** (port 443): Encrypted using TLS. Provides confidentiality, integrity, and authentication via certificates.

**SOC note**: Even HTTPS can be malicious (malware uses HTTPS for C2 to blend in). SSL inspection at the proxy level helps.

---

## 3. Common Protocols

### Q12. List commonly used ports and their protocols.

| Port | Protocol | Used For |
|---|---|---|
| 20/21 | FTP | File transfer |
| 22 | SSH | Secure remote access |
| 23 | Telnet | Insecure remote access |
| 25 | SMTP | Email sending |
| 53 | DNS | Domain name resolution |
| 80 | HTTP | Web traffic |
| 110 | POP3 | Email retrieval |
| 143 | IMAP | Email retrieval |
| 389 | LDAP | Directory services |
| 443 | HTTPS | Secure web traffic |
| 445 | SMB | File sharing (Windows) |
| 3306 | MySQL | Database |
| 3389 | RDP | Remote Desktop Protocol |
| 8080 | HTTP Alt | Web proxy/alternative web |

**Tip**: Know which ports are commonly exploited — 445 (EternalBlue/WannaCry), 3389 (RDP brute-force), 22 (SSH brute-force).

---

### Q13. What is ICMP and how is it used in attacks?

ICMP (Internet Control Message Protocol) is used for network diagnostics — e.g., `ping` uses ICMP Echo Request/Reply.

**Attack uses:**
- **Ping of Death**: Oversized ICMP packet crashes a system
- **ICMP Tunneling**: Data exfiltration by hiding data in ICMP payloads
- **Smurf Attack**: Amplification DDoS using ICMP broadcast

---

### Q14. What is SMTP and how can it be abused?

SMTP (Simple Mail Transfer Protocol) is used to send emails (port 25/587).

**Abuse vectors:**
- **Phishing emails** (spoofed sender domains)
- **Open relays**: Misconfigured SMTP servers that allow anyone to send email through them (spammers abuse this)
- **Email header injection**

---

## 4. Firewalls, IDS/IPS, and Network Security

### Q15. What is the difference between a firewall, IDS, and IPS?

| Device | Function | Action Taken |
|---|---|---|
| **Firewall** | Filters traffic based on rules (IP, port, protocol) | Allows or blocks traffic |
| **IDS** (Intrusion Detection System) | Monitors and detects suspicious activity | **Alerts only** — passive |
| **IPS** (Intrusion Prevention System) | Detects and actively prevents threats | **Blocks/drops** traffic — active |

**SOAR relevance**: IDS/IPS alerts are ingested by SIEM and can trigger SOAR playbooks for automated response.

---

### Q16. What is the difference between a stateful and stateless firewall?

- **Stateless**: Inspects each packet in isolation based on static rules (source/dest IP, port). No context of connection state.
- **Stateful**: Tracks the state of active connections. Only allows return traffic for established sessions. More intelligent and secure.

---

### Q17. What is a DMZ (Demilitarized Zone)?

A DMZ is a network segment between an internal network and the internet, hosting publicly accessible services (web servers, mail servers). It provides an additional layer of security so that even if a public-facing server is compromised, the attacker can't directly reach the internal network.

```
Internet → [Firewall] → DMZ (Web/Mail Servers) → [Firewall] → Internal Network
```

---

### Q18. What is a WAF (Web Application Firewall)?

A WAF operates at Layer 7 (Application layer) and filters HTTP/HTTPS traffic to protect web applications from attacks like:
- SQL Injection
- Cross-Site Scripting (XSS)
- CSRF
- Path Traversal

Examples: Cloudflare WAF, AWS WAF, F5 BIG-IP.

---

### Q19. What is network segmentation and why is it important?

Network segmentation divides a network into smaller zones/segments (using VLANs, subnets, firewalls).

**Benefits:**
- **Limits lateral movement**: If an attacker compromises one segment, they can't freely move to others.
- **Contains breaches**: Reduces blast radius.
- **Compliance**: Required for PCI-DSS (cardholder data must be in isolated segments).

---

## 5. Cryptography & PKI

### Q20. What is the difference between symmetric and asymmetric encryption?

| Feature | Symmetric | Asymmetric |
|---|---|---|
| Keys Used | Same key for encrypt/decrypt | Public key (encrypt) + Private key (decrypt) |
| Speed | Fast | Slow |
| Key Exchange | Problem (how to share securely?) | Solved (public key is shared openly) |
| Examples | AES, DES, 3DES | RSA, ECC, Diffie-Hellman |
| Use Case | Bulk data encryption | Key exchange, digital signatures, TLS |

**TLS uses both**: Asymmetric encryption to exchange a symmetric session key, then symmetric for the actual data transfer.

---

### Q21. What is hashing and how is it different from encryption?

- **Encryption**: Two-way — data can be decrypted with the right key.
- **Hashing**: One-way — converts data into a fixed-length digest. Cannot be reversed.

**Common hash algorithms:**
- **MD5** (128-bit) — broken, not recommended
- **SHA-1** (160-bit) — deprecated
- **SHA-256 / SHA-3** — currently recommended

**Uses in security:**
- Password storage (store hash, not plaintext)
- File integrity checks (IOC matching in SIEM)
- Digital signatures

---

### Q22. What is a digital certificate and how does PKI work?

A **digital certificate** binds a public key to an identity (domain, organization), signed by a trusted Certificate Authority (CA).

**PKI (Public Key Infrastructure) flow:**
1. Entity generates a key pair (public + private)
2. Submits a Certificate Signing Request (CSR) to a CA
3. CA verifies identity and issues a signed certificate
4. Browser/client trusts the cert because it trusts the CA (Root CA in trust store)

**SOC relevance**: Expired/self-signed/revoked certificates can be IoCs. TLS inspection requires deploying your own CA to decrypt traffic.

---

### Q23. What is the difference between SSL and TLS?

SSL (Secure Sockets Layer) is the predecessor to TLS (Transport Layer Security). SSL is deprecated (SSL 2.0, 3.0 are broken). Current standard is **TLS 1.2** and **TLS 1.3** (TLS 1.0/1.1 are also deprecated).

**POODLE, BEAST, DROWN** — known attacks against SSL/older TLS versions.

---

## 6. Threat Intelligence & Attack Frameworks

### Q24. What is the MITRE ATT&CK framework?

MITRE ATT&CK is a globally-accessible knowledge base of adversary tactics, techniques, and procedures (TTPs) based on real-world observations.

**Structure:**
- **Tactics**: The adversary's goal (e.g., Initial Access, Persistence, Lateral Movement, Exfiltration)
- **Techniques**: How the goal is achieved (e.g., T1566 - Phishing)
- **Sub-techniques**: More specific methods (e.g., T1566.001 - Spearphishing Attachment)

**SOAR use**: Map SIEM alerts and playbook triggers to ATT&CK techniques for structured incident classification and reporting.

---

### Q25. What is the Cyber Kill Chain?

Developed by Lockheed Martin, the Kill Chain describes the stages of a cyberattack:

1. **Reconnaissance** — Gathering target information
2. **Weaponization** — Creating malware/exploit
3. **Delivery** — Sending payload (phishing, USB, web)
4. **Exploitation** — Triggering the vulnerability
5. **Installation** — Malware installs itself
6. **Command & Control (C2)** — Attacker gains remote access
7. **Actions on Objectives** — Data theft, ransomware, destruction

**Use**: Identify at which stage an attack was detected to understand defensive gaps.

---

### Q26. What are Indicators of Compromise (IoCs)?

IoCs are pieces of forensic data that indicate a system may have been breached:
- **IP addresses** (known malicious C2 servers)
- **Domain names** (malware domains)
- **File hashes** (MD5/SHA-256 of malicious files)
- **URLs** (phishing URLs)
- **Registry keys** (persistence mechanisms)
- **Email addresses** (phishing senders)
- **User agent strings** (malicious tools)

**SIEM/SOAR use**: IoCs are ingested from threat intel feeds and matched against logs to trigger alerts and automated playbooks.

---

### Q27. What is STIX/TAXII?

- **STIX** (Structured Threat Information eXpression): A standardized language/format for describing cyber threat intelligence.
- **TAXII** (Trusted Automated eXchange of Indicator Information): A protocol for sharing STIX data between organizations.

**Use in SOAR**: XSOAR integrates with STIX/TAXII feeds to pull threat intel and enrich alerts automatically.

---

## 7. Incident Response Lifecycle

### Q28. What are the phases of the NIST Incident Response lifecycle?

**NIST SP 800-61** defines four phases:

1. **Preparation** — Tools, playbooks, team training, communication plans
2. **Detection & Analysis** — Identify and confirm the incident, determine scope and severity
3. **Containment, Eradication & Recovery**
   - *Containment*: Isolate affected systems to prevent spread
   - *Eradication*: Remove malware/attacker persistence
   - *Recovery*: Restore systems, verify they're clean, return to production
4. **Post-Incident Activity** — Lessons learned, update playbooks, report

---

### Q29. What is triage in incident response?

Triage is the process of quickly assessing and prioritizing incidents based on:
- **Severity** (Critical, High, Medium, Low)
- **Impact** (number of systems/users affected)
- **Type of attack** (ransomware vs. phishing vs. DDoS)

**SOAR role**: Playbooks automate triage — enriching alerts with threat intel, asset info, and user context to automatically classify and assign severity.

---

### Q30. What is the difference between an event, alert, and incident?

- **Event**: Any observable occurrence in a system (log entry, login attempt)
- **Alert**: An event that has been flagged as potentially malicious by a SIEM rule
- **Incident**: A confirmed security event that has caused or could cause harm to the organization

---

## 8. Vulnerability Management

### Q31. What is the difference between a vulnerability, threat, and risk?

- **Vulnerability**: A weakness in a system (e.g., unpatched software, misconfiguration)
- **Threat**: A potential actor or event that could exploit a vulnerability (e.g., ransomware group, insider threat)
- **Risk**: The likelihood and impact of a threat exploiting a vulnerability

```
Risk = Threat × Vulnerability × Impact
```

---

### Q32. What is CVE and CVSS?

- **CVE (Common Vulnerabilities and Exposures)**: A public database of known vulnerabilities with unique IDs (e.g., CVE-2021-44228 — Log4Shell)
- **CVSS (Common Vulnerability Scoring System)**: A scoring system (0-10) that rates severity of vulnerabilities.
  - **0-3.9**: Low
  - **4-6.9**: Medium
  - **7-8.9**: High
  - **9-10**: Critical

**SOAR use**: Vulnerability scanner findings (Qualys, Tenable) are ingested via SOAR integrations and CVSS scores are used to auto-prioritize remediation playbooks.

---

### Q33. What is the difference between a vulnerability scan and a penetration test?

| | Vulnerability Scan | Penetration Test |
|---|---|---|
| **Purpose** | Identify known vulnerabilities | Actively exploit vulnerabilities to assess real-world risk |
| **Who** | Usually automated tools | Skilled security professionals (red team) |
| **Depth** | Broad, shallow | Deep, targeted |
| **Tools** | Nessus, Qualys, OpenVAS | Metasploit, Burp Suite, custom exploits |
| **Frequency** | Regular (weekly/monthly) | Periodic (annual/quarterly) |

---

## 9. Identity & Access Management (IAM)

### Q34. What is the Principle of Least Privilege (PoLP)?

Users, systems, and processes should only have the minimum permissions required to perform their tasks. This limits damage from compromised accounts or insider threats.

**Example**: A helpdesk agent should not have domain admin rights.

---

### Q35. What is MFA and why is it important?

**MFA (Multi-Factor Authentication)** requires two or more of:
- **Something you know** (password)
- **Something you have** (OTP token, authenticator app, smart card)
- **Something you are** (biometrics)

**Why important**: Even if a password is stolen (phishing, credential stuffing), MFA prevents unauthorized access.

**Common bypass attacks**: SIM swapping, MFA fatigue/prompt bombing, adversary-in-the-middle phishing (e.g., Evilginx).

---

### Q36. What is the difference between authentication and authorization?

- **Authentication (AuthN)**: Verifying identity — "Who are you?" (username + password)
- **Authorization (AuthZ)**: Verifying permissions — "What are you allowed to do?" (role-based access control)

---

### Q37. What is Active Directory and why is it a target?

**Active Directory (AD)** is Microsoft's directory service for managing users, computers, and resources in a Windows domain.

**Why it's a target**: Compromising AD (especially Domain Admin accounts) gives attackers control over the entire organization.

**Common AD attacks:**
- **Pass-the-Hash (PtH)**: Use NTLM hash instead of plaintext password
- **Kerberoasting**: Extract service ticket hashes and crack offline
- **Golden Ticket**: Forge Kerberos tickets using the KRBTGT hash
- **DCSync**: Mimic domain controller to extract all password hashes

---

## 10. Log Analysis & SIEM Basics

### Q38. What types of logs are important in a SOC?

| Log Type | Source | What to Look For |
|---|---|---|
| **Windows Event Logs** | Endpoints, DCs | Failed logins (4625), account creation (4720), privilege escalation (4672) |
| **Firewall Logs** | Network perimeter | Unusual outbound connections, blocked traffic, port scans |
| **DNS Logs** | DNS servers | High-frequency queries, DGA domains, long TTL records |
| **Proxy/Web Logs** | Web proxy | Suspicious URLs, large data transfers, beaconing patterns |
| **VPN Logs** | VPN gateway | Logins from unusual locations, off-hours access |
| **Authentication Logs** | AD, LDAP, SSO | Brute force, lateral movement, privilege use |
| **EDR/AV Logs** | Endpoints | Malware detection, suspicious process execution |

---

### Q39. What is a SIEM and how does it work?

**SIEM (Security Information and Event Management)** centralizes log collection, correlation, alerting, and reporting.

**Core functions:**
1. **Log Collection**: Agents or syslog/API-based ingestion from diverse sources
2. **Normalization**: Parse different log formats into a common schema
3. **Correlation**: Apply rules to detect patterns across multiple events
4. **Alerting**: Generate alerts when correlation rules match
5. **Dashboards & Reports**: Visibility into security posture
6. **Retention**: Long-term storage for forensics and compliance

**Popular SIEMs**: Splunk, IBM QRadar, Microsoft Sentinel, ArcSight, Elastic SIEM.

---

### Q40. What is log normalization and why does it matter?

Different systems produce logs in different formats. Normalization maps raw log fields to a common schema (e.g., `src_ip`, `dst_ip`, `user`, `action`).

**Why it matters**: You can't correlate events across systems without a common data model. For example, matching a firewall block with an endpoint alert requires both to use the same field names.

---

## 11. Endpoint Security

### Q41. What is the difference between antivirus (AV) and EDR?

| | Antivirus (AV) | EDR |
|---|---|---|
| **Detection** | Signature-based | Behavioral, heuristic, ML-based |
| **Coverage** | Known malware | Known + unknown (zero-day) |
| **Response** | Quarantine/delete | Isolation, process kill, rollback |
| **Visibility** | Limited | Full process tree, file, network, registry |
| **Examples** | McAfee, Norton | CrowdStrike Falcon, SentinelOne, Microsoft Defender ATP |

---

### Q42. What is process injection?

Process injection is a technique where malicious code is inserted into a legitimate running process (e.g., `svchost.exe`, `explorer.exe`) to evade detection.

**Common types:**
- **DLL Injection**: Inject a malicious DLL into a process
- **Process Hollowing**: Replace legitimate process code with malware
- **Reflective DLL Injection**: Load DLL from memory without writing to disk

**Detection**: Monitor for unusual parent-child process relationships, unexpected memory allocation in trusted processes.

---

## 12. Common Attack Types

### Q43. What is phishing? What are its variants?

**Phishing**: Fraudulent communication (usually email) that tricks users into revealing credentials or installing malware.

| Variant | Description |
|---|---|
| **Spear Phishing** | Targeted at a specific individual/org (highly personalized) |
| **Whaling** | Targets C-suite executives |
| **Vishing** | Voice/phone phishing |
| **Smishing** | SMS phishing |
| **Business Email Compromise (BEC)** | Impersonating executives for financial fraud |

---

### Q44. What is a Man-in-the-Middle (MitM) attack?

An attacker secretly intercepts and potentially alters communication between two parties without their knowledge.

**Methods:**
- ARP Poisoning
- SSL Stripping (downgrade HTTPS to HTTP)
- Rogue Wi-Fi (Evil Twin access point)
- DNS Spoofing

**Prevention**: HTTPS, MFA, HSTS, certificate pinning, network monitoring.

---

### Q45. What is a DDoS attack and types?

**DDoS (Distributed Denial of Service)**: Overwhelming a target with traffic from multiple sources to make it unavailable.

| Type | Description | Example |
|---|---|---|
| **Volumetric** | Flood with massive traffic | UDP flood, ICMP flood |
| **Protocol** | Exhaust network resources | SYN flood, Ping of Death |
| **Application Layer** | Target web app resources | HTTP flood (Layer 7) |
| **Amplification** | Use open servers to amplify traffic | DNS amplification, NTP amplification |

---

### Q46. What is SQL injection?

SQL injection occurs when an attacker inserts malicious SQL code into an input field, manipulating the database query.

**Example:**
```
Input: ' OR '1'='1
Query: SELECT * FROM users WHERE username='' OR '1'='1'
```
This bypasses authentication by making the condition always true.

**Prevention**: Parameterized queries/prepared statements, input validation, WAF, least privilege DB accounts.

---

### Q47. What is Cross-Site Scripting (XSS)?

XSS is a client-side injection attack where malicious scripts are injected into web pages viewed by other users.

| Type | Description |
|---|---|
| **Stored XSS** | Script permanently stored on server (DB) |
| **Reflected XSS** | Script reflected off server in response |
| **DOM-based XSS** | Script modifies the DOM in the browser |

**Impact**: Cookie theft, session hijacking, defacement, credential harvesting.

---

### Q48. What is ransomware and how does it work?

Ransomware is malware that encrypts a victim's files and demands a ransom for the decryption key.

**Attack chain:**
1. Initial access (phishing, RDP brute-force, vulnerability exploitation)
2. Privilege escalation (gain admin/domain admin)
3. Lateral movement (spread across network)
4. Data exfiltration (double extortion — steal data before encrypting)
5. Encryption (encrypt files, delete backups/VSS)
6. Ransom demand

**Famous examples**: WannaCry, REvil, LockBit, Conti, BlackCat.

**SOAR response**: Automated isolation of infected hosts, blocking C2 IPs, disabling compromised accounts.

---

### Q49. What is lateral movement?

Lateral movement refers to techniques attackers use to progressively move through a network to reach high-value targets (e.g., domain controller, financial systems) after gaining initial access.

**Common techniques:**
- **Pass-the-Hash (PtH)**
- **Pass-the-Ticket (PtT)**
- **Remote Service exploitation** (RDP, SMB, WMI, PsExec)
- **Living off the Land (LotL)**: Using built-in tools like PowerShell, WMI, net.exe

**Detection**: Unusual lateral connections, use of admin tools from non-admin workstations, after-hours logins.

---

### Q50. What is privilege escalation?

Privilege escalation is gaining higher-level permissions than initially granted.

- **Horizontal**: Accessing resources of another user at the same privilege level
- **Vertical**: Gaining higher privileges (e.g., user → admin → SYSTEM/root)

**Common techniques:**
- Exploiting misconfigured sudo permissions (Linux)
- Unquoted service paths, DLL hijacking (Windows)
- Token impersonation
- Kernel exploits

---

## 🎯 Quick Interview Tips

1. **Always relate your answers back to SOC/SIEM/SOAR context** — show you understand why these concepts matter operationally.
2. **Use the STAR method** for scenario-based questions (Situation, Task, Action, Result).
3. **Know your attack frameworks** — MITRE ATT&CK will come up repeatedly.
4. **Be comfortable with log analysis** — understand what Windows Event IDs like 4624, 4625, 4688, 4672, 4720 mean.
5. **Acknowledge limits honestly** — it's okay to say "I haven't worked with X directly but here's how I'd approach it."

---

## 📌 Key Windows Event IDs to Remember

| Event ID | Description |
|---|---|
| 4624 | Successful logon |
| 4625 | Failed logon |
| 4648 | Logon using explicit credentials |
| 4672 | Special privileges assigned (admin logon) |
| 4688 | New process created |
| 4698 | Scheduled task created |
| 4720 | User account created |
| 4728/4732 | User added to security group |
| 4776 | NTLM authentication attempt |
| 7045 | New service installed |

---

*Last Updated: August 2026 | Tailored for Deloitte T&T Cyber D&R XSOAR Consultant Interview | Omkar Jadhav — Security Integration & Automation Engineer*
