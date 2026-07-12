# 🛡️ Suricata IDS Alert

This document explains the implementation of the **Suricata IDS Detection Alert** within the Splunk SOC Home Lab.

The purpose of this detection is to identify suspicious network activities, such as **port scanning and reconnaissance**, using **Suricata Intrusion Detection System (IDS)**. When malicious traffic is detected, the alert is forwarded to Splunk Enterprise, visualized on the SOC Dashboard, and an automated email notification is sent to the analyst.

This demonstrates a complete **Network Detection and Response (NDR)** workflow integrated with a SIEM platform.

---

# 🎯 Objectives

The objectives of this detection are:

- Detect network reconnaissance activities
- Monitor suspicious network traffic
- Forward IDS alerts to Splunk Enterprise
- Visualize alerts in the SOC Dashboard
- Automatically notify SOC analysts via email
- Validate the complete IDS → SIEM → Alert pipeline

---

# 🏗️ Detection Architecture

```
              Kali Linux
             (Nmap Scan)
                  │
                  ▼
        Ubuntu Endpoint
                  │
                  ▼
           Suricata IDS
                  │
          eve.json Alerts
                  │
                  ▼
   Splunk Universal Forwarder
                  │
                  ▼
      Splunk Enterprise Server
                  │
        ┌─────────┴─────────┐
        ▼                   ▼
 Dashboard Studio      Email Alert
        │                   │
        └─────────┬─────────┘
                  ▼
           SOC Investigation
```

---

# 🛡️ MITRE ATT&CK Mapping

| Technique | ID |
|------------|----|
| Active Scanning | T1595 |
| Network Service Discovery | T1046 |
| Discovery | TA0007 |

---

# 📂 Data Source

**Operating System**

- Ubuntu 22.04

**Detection Engine**

- Suricata IDS

**Log File**

```
/var/log/suricata/eve.json
```

**Splunk Sourcetype**

```
suricata
```

---

# 🔍 Detection Logic

Suricata continuously monitors network traffic flowing through the Ubuntu endpoint.

When suspicious traffic matches one of its detection rules, it generates an alert in **eve.json**, which is monitored by the Splunk Universal Forwarder and forwarded to Splunk Enterprise.

The alert is then indexed, visualized in the dashboard, and evaluated against configured alert rules.

---

# 🔍 SPL Detection Query

```spl
index=* sourcetype=suricata
| stats count by alert.signature, src_ip, dest_ip, severity
| sort - count
```

### Example Detection Query (Nmap)

```spl
index=* sourcetype=suricata
alert.signature="*Nmap*"
```

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

When Suricata detects suspicious network activity, Splunk automatically sends an email notification.

### Email Includes

- Alert Name
- Detection Time
- Source IP
- Destination IP
- Alert Signature
- Severity
- Protocol
- Event Details

This enables analysts to immediately begin investigating the event.

---

# ⚔️ Attack Validation

## Attacker Machine

- Kali Linux

### Tool Used

- Nmap

### Target

- Ubuntu Endpoint

---

## Attack Flow

```
Nmap Scan

↓

Ubuntu Endpoint

↓

Suricata IDS

↓

eve.json

↓

Splunk Universal Forwarder

↓

Splunk Enterprise

↓

Detection Rule

↓

SOC Dashboard

↓

Email Alert

↓

SOC Analyst
```

---

# 📊 Dashboard Response

Once the alert is generated, the SOC Dashboard updates automatically.

Affected dashboard panels include:

- IDS Alert Counter
- Threat Timeline
- Alert Severity
- Top Attack Signatures
- Top Source IPs
- Top Destination IPs
- Risk Score
- Live Investigation Panel

This provides analysts with immediate visibility into the detected activity.

---

# 📨 Sample Alert Information

| Field | Example |
|--------|---------|
| Alert Name | Suricata IDS Detection |
| Severity | High |
| Source IP | 192.168.1.103 |
| Destination IP | 192.168.1.102 |
| Protocol | TCP |
| Signature | ET SCAN Nmap Scripting Engine User-Agent |
| Detection Time | 2026-07-12 15:10:42 |

---

# 💡 Why This Detection Matters

Reconnaissance is often the **first stage of a cyber attack**. Attackers perform network scans to identify:

- Open Ports
- Running Services
- Operating Systems
- Vulnerable Applications

Detecting reconnaissance activity early allows defenders to identify attackers before exploitation begins.

By integrating Suricata IDS with Splunk Enterprise, the SOC gains real-time visibility into suspicious network behavior and can respond more quickly to potential threats.

---

# ✅ Validation Checklist

Confirm the following during testing:

- Suricata service is running
- eve.json is generated
- Universal Forwarder monitors eve.json
- Events appear in Splunk
- Detection rule triggers successfully
- Dashboard updates correctly
- Email notification is received

---

# 🔧 Troubleshooting

## No Alerts Generated

- Verify Suricata is running.
- Check HOME_NET configuration.
- Ensure detection rules are enabled.
- Confirm traffic passes through the monitored interface.

---

## eve.json Not Updating

Verify:

```
/var/log/suricata/eve.json
```

exists and contains events.

Restart Suricata if necessary.

---

## Events Not Appearing in Splunk

Verify the Universal Forwarder is monitoring:

```
/var/log/suricata/eve.json
```

Restart the forwarder after updating **inputs.conf**.

---

## Email Alert Not Received

- Verify SMTP configuration.
- Test Splunk email settings.
- Ensure the detection query returns matching events.

---

# 🚀 Future Improvements

Planned enhancements include:

- Malware Detection Rules
- DNS Tunneling Detection
- HTTP Threat Detection
- TLS Anomaly Detection
- Command & Control (C2) Detection
- Threat Intelligence Integration
- Risk-Based Alerting
- SOAR Automation
- Automated IP Reputation Lookup

---

# 📸 Suggested Screenshots

Include screenshots of:

- Nmap Scan Execution
- Suricata Console
- eve.json Events
- Splunk Search Results
- IDS Dashboard Panel
- Triggered Email Alert
- Alert Configuration
- Risk Score Update

---

# 📚 Related Documentation

- README.md
- Installation.md
- Dashboard-Setup.md
- Email-Alerting.md
- Attack-Simulation.md
- brute-force-alert.md
- Troubleshooting.md