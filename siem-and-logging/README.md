# SIEM & Log Management

## Why This Matters

If you can't see it, you can't defend it. A SIEM (Security Information and Event Management) platform collects logs from across your environment, correlates events, and alerts you when something looks wrong. This is the foundation of security operations.

## What Logs to Collect (Minimum)

Start with these — they cover the most common attack paths:

### High Priority
- **Authentication logs** - Active Directory, VPN, SSO (failed logins, account lockouts, privilege escalation)
- **Firewall logs** - Allowed/denied connections, especially outbound
- **Endpoint detection logs** - EDR alerts, antivirus detections
- **Email gateway logs** - Phishing attempts, blocked attachments, suspicious links
- **DNS logs** - Query logs help detect C2 communication and data exfiltration

### Medium Priority
- **Web proxy logs** - URL filtering, blocked categories, unusual user-agents
- **Cloud platform logs** - AWS CloudTrail, Azure Activity Log, GCP Audit Logs
- **Application logs** - Critical business applications, databases
- **DHCP logs** - IP-to-hostname mapping for investigations

### Nice to Have
- **File integrity monitoring** - Changes to critical system files
- **Network flow data** - NetFlow/sFlow for traffic analysis
- **Badge/physical access logs** - Correlate physical and logical access

## Platform Comparison

### Splunk
- **Best for**: Large enterprises with budget, complex queries
- **Query language**: SPL (Search Processing Language)
- **Pricing**: Per GB ingested (can get expensive fast)
- **Tip**: Start with a free Splunk license (500 MB/day) to learn SPL

### Microsoft Sentinel
- **Best for**: Organizations heavy on Microsoft/Azure
- **Query language**: KQL (Kusto Query Language)
- **Pricing**: Pay per GB ingested + analytics rules
- **Tip**: Use built-in connectors for M365 and Azure — they're easy wins

### Elastic Security (ELK)
- **Best for**: Teams that want flexibility and open-source options
- **Query language**: KQL (Kibana Query Language) and Lucene
- **Pricing**: Free self-managed, paid for cloud/support
- **Tip**: Use Elastic Agent for simplified endpoint log collection

### Wazuh
- **Best for**: Smaller teams, budget-conscious organizations
- **Capabilities**: HIDS + SIEM + compliance monitoring
- **Pricing**: Completely free and open source
- **Tip**: Great starter SIEM — deploy it to learn before moving to enterprise tools

## Detection Rules to Start With

These cover the most common attack techniques (mapped to MITRE ATT&CK):

1. **Brute force detection** - Multiple failed logins from same source (T1110)
2. **Impossible travel** - Same user logging in from distant locations (T1078)
3. **New admin account created** - Unexpected privilege grants (T1136)
4. **PowerShell encoded commands** - Base64 encoded execution (T1059.001)
5. **Large outbound data transfer** - Potential exfiltration (T1048)
6. **Login outside business hours** - From sensitive accounts (T1078)
7. **Disabled security tools** - EDR/AV tampered with (T1562)
8. **New scheduled task/service** - Persistence mechanisms (T1053)

## Log Retention Guidelines

| Log Type | Minimum Retention | Recommended |
|----------|------------------|-------------|
| Authentication | 90 days | 1 year |
| Firewall | 90 days | 6 months |
| EDR/AV | 90 days | 1 year |
| DNS | 30 days | 90 days |
| Email | 90 days | 1 year |
| Cloud audit | 90 days | 1 year |

Check your industry's compliance requirements — PCI DSS, HIPAA, SOX, etc. may require longer retention.
