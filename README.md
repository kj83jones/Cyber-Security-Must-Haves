# Cyber Security Must-Haves

A curated collection of essential tools, frameworks, checklists, and playbooks for security operations. Built from real-world SecOps experience.

## Who This Is For

- Security Operations Center (SOC) analysts
- Incident responders
- Security engineers
- Anyone building or improving a security program

## Repository Structure

```
.
├── siem-and-logging/        # SIEM platforms, log management, and detection rules
├── incident-response/       # IR playbooks, runbooks, and templates
├── network-security/        # Firewalls, IDS/IPS, network monitoring tools
├── endpoint-security/       # EDR, antivirus, host hardening
└── README.md
```

## Quick Reference - Essential Tool Categories

### 1. SIEM & Log Management
Centralized logging and alerting is the backbone of any SOC. See [`siem-and-logging/`](siem-and-logging/) for detailed guidance.

| Tool | Type | Notes |
|------|------|-------|
| Splunk | Commercial SIEM | Industry standard, powerful SPL query language |
| Microsoft Sentinel | Cloud SIEM | Native Azure integration, KQL queries |
| Elastic Security | Open/Commercial | ELK stack based, flexible and scalable |
| Wazuh | Open Source | HIDS + SIEM, great for smaller teams |
| Graylog | Open Source | Solid log management with alerting |

### 2. Incident Response
Having a plan before an incident happens is non-negotiable. See [`incident-response/`](incident-response/) for playbooks.

| Tool | Type | Notes |
|------|------|-------|
| TheHive | Open Source | Case management for IR teams |
| Cortex | Open Source | Observable analysis automation (pairs with TheHive) |
| Velociraptor | Open Source | Endpoint visibility and forensic collection |
| DFIR-IRIS | Open Source | Incident response case management platform |

### 3. Network Security
Visibility into your network is critical. See [`network-security/`](network-security/) for tools and checklists.

| Tool | Type | Notes |
|------|------|-------|
| Suricata | Open Source | IDS/IPS, network threat detection |
| Zeek (Bro) | Open Source | Network analysis and logging framework |
| pfSense / OPNsense | Open Source | Firewall platforms |
| Wireshark | Open Source | Packet analysis, every analyst should know this |
| Nmap | Open Source | Network discovery and security auditing |

### 4. Endpoint Security
Protect what the users touch. See [`endpoint-security/`](endpoint-security/) for hardening guides.

| Tool | Type | Notes |
|------|------|-------|
| CrowdStrike Falcon | Commercial EDR | Leading EDR platform |
| Microsoft Defender for Endpoint | Commercial EDR | Strong if you're in the Microsoft ecosystem |
| SentinelOne | Commercial EDR | AI-driven threat detection |
| OSSEC / Wazuh Agent | Open Source | Host-based intrusion detection |
| Sysmon | Free (Microsoft) | Detailed Windows event logging, essential for detection |

### 5. Vulnerability Management

| Tool | Type | Notes |
|------|------|-------|
| Nessus | Commercial | Industry standard vulnerability scanner |
| OpenVAS / Greenbone | Open Source | Full-featured vulnerability scanner |
| Qualys | Commercial | Cloud-based vuln management platform |
| Nuclei | Open Source | Fast, template-based vulnerability scanner |

### 6. Threat Intelligence

| Tool | Type | Notes |
|------|------|-------|
| MISP | Open Source | Threat intelligence sharing platform |
| OpenCTI | Open Source | Cyber threat intelligence platform |
| VirusTotal | Free/Commercial | File and URL analysis |
| AbuseIPDB | Free/Commercial | IP reputation checking |
| Shodan | Free/Commercial | Internet-connected device search engine |

## Frameworks & Standards

These frameworks guide how to build and measure a security program:

- **NIST Cybersecurity Framework (CSF)** - Identify, Protect, Detect, Respond, Recover
- **MITRE ATT&CK** - Adversary tactics and techniques knowledge base
- **CIS Controls** - Prioritized set of security best practices
- **ISO 27001** - Information security management standard
- **NIST 800-53** - Security and privacy controls catalog

## Contributing

This is a living document. If you have tools or resources to add, open a pull request or issue.

## License

This project is open source and available under the [MIT License](LICENSE).
