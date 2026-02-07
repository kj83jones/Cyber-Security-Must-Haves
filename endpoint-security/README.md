# Endpoint Security

## Why This Matters

Endpoints — laptops, desktops, servers — are where users work and where attackers land. A phishing email delivers a payload to an endpoint. A vulnerable application gets exploited on an endpoint. Endpoint security is your last line of defense when perimeter controls fail.

## Endpoint Security Checklist

### Baseline Hardening
- [ ] Remove local admin rights from standard users
- [ ] Enable host-based firewall (Windows Firewall, iptables)
- [ ] Disable unnecessary services and protocols (SMBv1, LLMNR, NetBIOS)
- [ ] Enable full disk encryption (BitLocker, FileVault, LUKS)
- [ ] Configure automatic screen lock (15 minutes max)
- [ ] Enforce application allowlisting on critical systems (AppLocker, WDAC)

### Patching
- [ ] OS patches within 14 days of release (7 days for critical)
- [ ] Third-party application patching (browsers, Java, Adobe, etc.)
- [ ] Firmware updates on a regular schedule
- [ ] Track patch compliance — aim for 95%+ within SLA

### Endpoint Detection & Response (EDR)
- [ ] Deploy EDR to all endpoints (servers and workstations)
- [ ] Ensure EDR is not in "monitor only" mode on production systems
- [ ] Configure EDR to block known malicious behaviors
- [ ] Review EDR alerts daily
- [ ] Test EDR detection with safe tools (Atomic Red Team)

### Windows-Specific Hardening
- [ ] Enable PowerShell script block logging (Event ID 4104)
- [ ] Enable PowerShell module logging
- [ ] Deploy Sysmon with a tuned configuration (SwiftOnSecurity or Olaf Hartong config)
- [ ] Disable LLMNR and NetBIOS Name Service
- [ ] Enable Credential Guard on supported systems
- [ ] Configure Windows Event log sizes (increase from defaults)
- [ ] Enable command-line process auditing (Event ID 4688)

### Linux-Specific Hardening
- [ ] Enable auditd with a comprehensive rule set
- [ ] Disable root SSH login (PermitRootLogin no)
- [ ] Use SSH key authentication (disable password auth)
- [ ] Configure fail2ban for brute force protection
- [ ] Set appropriate file permissions (no world-writable directories)
- [ ] Enable SELinux or AppArmor

## Windows Event IDs Every SOC Analyst Should Know

| Event ID | Source | What It Means |
|----------|--------|---------------|
| 4624 | Security | Successful logon |
| 4625 | Security | Failed logon |
| 4648 | Security | Logon using explicit credentials (runas) |
| 4672 | Security | Admin/special privileges assigned to logon |
| 4688 | Security | New process created (with command line if auditing enabled) |
| 4697 | Security | New service installed |
| 4698 | Security | Scheduled task created |
| 4720 | Security | User account created |
| 4732 | Security | User added to a security group |
| 7045 | System | New service installed |
| 4104 | PowerShell | Script block logging (see the actual script content) |
| 1 | Sysmon | Process creation (better than 4688) |
| 3 | Sysmon | Network connection |
| 11 | Sysmon | File creation |
| 13 | Sysmon | Registry value set |

## EDR Platform Comparison

### CrowdStrike Falcon
- **Strengths**: Industry-leading detection, excellent threat intelligence, cloud-native
- **Considerations**: Premium pricing, requires CrowdStrike cloud connectivity
- **Best for**: Organizations that want best-in-class detection

### Microsoft Defender for Endpoint
- **Strengths**: Native Windows integration, included in M365 E5, good API
- **Considerations**: Windows-centric (Linux/Mac support improving)
- **Best for**: Microsoft-heavy environments already on E5 licensing

### SentinelOne
- **Strengths**: Autonomous response, good Linux support, rollback capability
- **Considerations**: Can be aggressive with automated responses
- **Best for**: Teams that want more automated response actions

### Carbon Black (VMware)
- **Strengths**: Strong process tree visibility, good for hunting
- **Considerations**: VMware acquisition uncertainty
- **Best for**: Organizations doing proactive threat hunting

## Testing Your Defenses

Use these frameworks to safely test if your endpoint security actually works:

| Tool | Purpose |
|------|---------|
| Atomic Red Team | Execute individual MITRE ATT&CK techniques |
| MITRE Caldera | Automated adversary emulation |
| Infection Monkey | Breach and attack simulation |
| Purple Knight | Active Directory security assessment |

Run these tests regularly. If your EDR doesn't alert, you have a gap.
