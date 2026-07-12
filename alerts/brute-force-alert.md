# 🚨 Windows Brute Force Alert

This document explains the **Windows Brute Force Detection Alert** configured in the Splunk SOC Home Lab.

The objective of this alert is to detect repeated failed authentication attempts against Windows systems and immediately notify SOC analysts through automated email alerts.

The alert simulates one of the most common attack techniques used by attackers attempting to gain unauthorized access.

---

# 🎯 Objective

The primary objectives of this alert are:

- Detect brute force login attempts
- Identify repeated authentication failures
- Notify SOC analysts immediately
- Reduce incident response time
- Demonstrate real-world SOC detection workflows

---

# 🏗 Detection Workflow

```
                Kali Linux
                 (Hydra)
                     │
                     ▼
          Windows Authentication
                     │
                     ▼
         Windows Security Logs
           (Event ID 4625)
                     │
                     ▼
     Splunk Universal Forwarder
                     │
                     ▼
         Splunk Enterprise Server
                     │
                     ▼
          Detection Rule Triggered
                     │
        ┌────────────┴─────────────┐
        ▼                          ▼
 Dashboard Studio           Email Alert
        │                          │
        └────────────┬─────────────┘
                     ▼
               SOC Investigation
```

---

# 🛡 MITRE ATT&CK Mapping

| Technique | ID |
|------------|----|
| Brute Force | T1110 |
| Credential Access | TA0006 |

---

# 📂 Data Source

**Operating System**

- Windows 10

**Log Source**

- Windows Security Logs

**Sourcetype**

```
WinEventLog:Security
```

---

# 📌 Detection Logic

Windows records every failed authentication attempt as:

```
Event ID: 4625
```

When multiple Event ID **4625** events are generated within a short period, the activity may indicate a brute force attack.

The detection rule monitors the frequency of these events and triggers an alert once the configured threshold is exceeded.

---

# 🔍 SPL Detection Query

```spl
index=* sourcetype="WinEventLog:Security" EventCode=4625
| stats count by Account_Name, Source_Network_Address, host
| where count >= 5
| sort - count
```

> **Note:** Adjust the threshold (`count >= 5`) based on your environment to reduce false positives.

---

# 🚨 Alert Configuration

| Setting | Value |
|----------|-------|
| Alert Type | Scheduled |
| Trigger | Number of Results > 0 |
| Schedule | Every 5 Minutes |
| Severity | High |
| Action | Send Email |

---

# 📧 Email Notification

When the detection rule is triggered, Splunk automatically sends an email notification.

### Email Includes

- Alert Name
- Detection Time
- Hostname
- Username
- Source IP Address
- Failed Login Count
- Event Details

This allows analysts to quickly assess the incident without opening Splunk.

---

# ⚔ Attack Validation

## Attacker Machine

- Kali Linux

### Tool Used

- Hydra

### Attack Target

- Windows Endpoint

### Attack Flow

```
Hydra

↓

Windows Login

↓

Failed Authentication

↓

Event ID 4625

↓

Splunk Universal Forwarder

↓

Splunk Enterprise

↓

Detection Rule

↓

Dashboard Update

↓

Email Alert

↓

SOC Analyst
```

---

# 📊 Dashboard Response

After the alert is triggered, the SOC Dashboard updates automatically.

Affected panels include:

- Failed Login Counter
- Security Event Timeline
- Risk Score
- Top Source IPs
- Live Investigation Panel
- Windows Authentication Events

This provides analysts with immediate visibility into the attack.

---

# 📨 Sample Alert Information

| Field | Example |
|--------|---------|
| Alert Name | Windows Brute Force Detection |
| Severity | High |
| Host | WIN10-ENDPOINT |
| Source IP | 192.168.1.103 |
| Event ID | 4625 |
| Failed Attempts | 12 |
| Detection Time | 2026-07-12 14:35:20 |

---

# 💡 Why This Detection Matters

Brute force attacks are commonly used to compromise user accounts by repeatedly guessing passwords.

Detecting these attempts early enables organizations to:

- Block malicious IP addresses
- Lock compromised accounts
- Prevent unauthorized access
- Reduce attack dwell time
- Improve incident response

Automated detection and alerting help ensure these attacks are identified even when analysts are not actively monitoring the dashboard.

---

# ✅ Validation Checklist

Confirm the following during testing:

- Windows Security logs are ingested into Splunk
- Event ID 4625 is generated
- Detection rule triggers successfully
- Dashboard updates in real time
- Email notification is received
- Relevant event details are available for investigation

---

# 🔧 Troubleshooting

### Alert Does Not Trigger

- Verify Windows auditing is enabled.
- Confirm Event ID 4625 events are being indexed.
- Check the alert search time range.
- Validate the SPL query returns results.

### Email Not Received

- Verify SMTP configuration.
- Confirm Gmail App Password is configured correctly.
- Test Splunk email settings.

### Dashboard Not Updating

- Ensure dashboard panels reference the correct index and sourcetype.
- Verify the time picker includes the attack period.

---

# 🚀 Future Improvements

Planned enhancements include:

- Password Spray Detection
- Account Lockout Detection
- Impossible Travel Detection
- Multi-Host Brute Force Correlation
- Risk-Based Alerting
- Threat Intelligence Enrichment
- SOAR Integration for Automated Response

---

# 📸 Suggested Screenshots

Add the following screenshots to this document:

- Hydra Brute Force Command
- Windows Event Viewer (Event ID 4625)
- Splunk Search Results
- Triggered Alert Rule
- Dashboard After Detection
- Email Notification
- Risk Score Increase

---

# 📚 Related Documentation

- README.md
- Installation.md
- Dashboard-Setup.md
- Email-Alerting.md
- Attack-Simulation.md
- suricata-alert.md
- Troubleshooting.md