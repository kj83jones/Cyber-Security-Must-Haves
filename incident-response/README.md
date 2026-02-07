# Incident Response

## Why This Matters

Every organization will face a security incident. The difference between a minor event and a catastrophe is how prepared you are. Having playbooks written *before* an incident means you're not making critical decisions under pressure.

## IR Phases (NIST SP 800-61)

```
1. Preparation       →  Get ready before incidents happen
2. Detection         →  Identify that something is wrong
3. Containment       →  Stop the bleeding
4. Eradication       →  Remove the threat
5. Recovery          →  Get back to normal
6. Lessons Learned   →  Improve for next time
```

## Incident Severity Levels

Define these ahead of time so everyone speaks the same language:

| Severity | Description | Example | Response Time |
|----------|-------------|---------|---------------|
| **SEV-1 (Critical)** | Active breach, data exfiltration, ransomware | Ransomware encrypting production servers | Immediate, all hands |
| **SEV-2 (High)** | Confirmed compromise, no active spread | Compromised user account with admin access | Within 1 hour |
| **SEV-3 (Medium)** | Suspicious activity, potential threat | Phishing email clicked, no confirmed compromise | Within 4 hours |
| **SEV-4 (Low)** | Minor security event | Failed brute force attempt, blocked malware | Next business day |

## Playbook: Phishing Response

This is the most common incident type you'll deal with.

### Detection
- User reports suspicious email
- Email gateway flags message
- SIEM alert on known malicious indicators

### Analysis
1. **Do NOT click links or open attachments** on your workstation
2. Get the full email headers (original .eml file if possible)
3. Check the sender domain — is it spoofed? Look-alike domain?
4. Extract URLs and check against threat intel (VirusTotal, URLScan.io)
5. Extract attachment hashes (SHA256) and check against threat intel
6. Determine: did anyone click the link / open the attachment?

### Containment
1. Block the sender domain/address at the email gateway
2. Block malicious URLs at the web proxy/firewall
3. Search mailboxes for same message delivered to other users
4. Delete/quarantine the message from all mailboxes
5. If credentials were entered: force password reset immediately
6. If malware was downloaded: isolate the endpoint

### Recovery
1. Re-image endpoint if malware executed
2. Monitor affected accounts for suspicious activity (30 days)
3. Verify no persistence mechanisms were installed

### Documentation
- Record the timeline of events
- Note IOCs (indicators of compromise) for future detection rules
- Update email filtering rules

## Playbook: Compromised Account

### Detection
- Impossible travel alert
- Login from known malicious IP
- Unusual activity (mass email, file access, privilege changes)

### Analysis
1. Identify the account and when compromise likely started
2. Review authentication logs — where did they log in from?
3. Review activity logs — what did they access?
4. Check for mail forwarding rules added to the account
5. Check for OAuth app consents or API keys created

### Containment
1. Reset the password immediately
2. Revoke all active sessions/tokens
3. Enable or re-enroll MFA
4. Disable the account if needed during investigation
5. Remove suspicious mail forwarding rules
6. Revoke any OAuth consents you don't recognize

### Recovery
1. Have the user set a new, strong password
2. Review and restore any data that was modified/deleted
3. Monitor for re-compromise (30 days)

## Playbook: Ransomware

### Detection
- EDR alerts on encryption behavior
- Users reporting inability to open files
- Ransom note files appearing on systems

### Containment (Act Fast)
1. **Isolate affected systems from the network immediately**
2. Disable shared drives/network shares to prevent spread
3. Identify patient zero — where did it start?
4. Preserve evidence before wiping anything
5. Do NOT pay the ransom without executive/legal involvement

### Eradication
1. Identify the ransomware variant (ID Ransomware, No More Ransom)
2. Determine the entry point (phishing, RDP, vulnerability)
3. Remove malware and persistence mechanisms
4. Patch the vulnerability that was exploited

### Recovery
1. Restore from clean, verified backups
2. Rebuild systems that can't be verified as clean
3. Restore in stages — critical systems first
4. Monitor for re-infection

## Essential IR Tools

| Tool | Purpose |
|------|---------|
| TheHive | Case management — track incidents and tasks |
| Velociraptor | Remote endpoint forensic collection |
| KAPE | Automated evidence collection (Windows) |
| Autoruns | Check persistence on Windows endpoints |
| Process Monitor | Real-time file/registry/process monitoring |
| CyberChef | Decode/deobfuscate data (GCHQ's Swiss army knife) |

## Communication During Incidents

- Use an out-of-band communication channel (not corporate email if email is compromised)
- Keep a running timeline of actions taken
- Brief leadership at regular intervals
- Coordinate with legal before any external communication
- Preserve evidence — don't wipe systems until forensics is done
