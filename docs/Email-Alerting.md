# 📧 Email Alerting Configuration

This document explains the implementation of **Email Alerting** within the Splunk SOC Home Lab.

In a real Security Operations Center (SOC), analysts cannot continuously monitor dashboards 24/7. To ensure critical security incidents are detected immediately, Splunk is configured to automatically send email notifications whenever predefined security conditions are met.

This transforms the dashboard from a passive monitoring tool into a proactive incident detection platform.

---

# 🎯 Objectives

The primary objectives of email alerting are:

- Notify analysts immediately when suspicious activity is detected.
- Reduce incident response time.
- Eliminate the need for continuous dashboard monitoring.
- Ensure high-priority security events are never missed.
- Simulate real-world SOC alerting workflows.

---

# 🏗 Alerting Architecture

```
Windows Endpoint
(Security Logs + Sysmon)
            │
            ▼

Splunk Universal Forwarder

            │

            ▼

       Splunk Enterprise
            │
            ▼

    Detection Rule Triggered

            │
            ▼

      Email Alert Generated

            │
            ▼

      SOC Analyst Notified
```

```
Ubuntu Endpoint
(Syslog + Suricata IDS)

            │
            ▼

Splunk Universal Forwarder

            │
            ▼

       Splunk Enterprise

            │
            ▼

    IDS Detection Triggered

            │
            ▼

      Email Alert Generated

            │
            ▼

      SOC Analyst Notified
```

---

# ⚙️ SMTP Configuration

Splunk Enterprise was configured to use Gmail SMTP for sending security notifications.

### Configuration

| Setting | Value |
|----------|-------|
| SMTP Server | smtp.gmail.com |
| Port | 587 |
| Encryption | TLS |
| Authentication | Gmail App Password |
| Sender | Configured Gmail Account |

> **Note:** Gmail App Passwords are recommended instead of using the primary account password.

---

# 🚨 Configured Alerts

Three security alerts were configured in this project.

---

## 1️⃣ Windows Brute Force Detection

### Purpose

Detect repeated failed login attempts against the Windows endpoint.

### Data Source

- Windows Security Logs

### Detection Logic

Monitor Windows Event ID:

```
4625
```

Trigger when multiple failed authentication attempts occur within a short period.

### Alert Action

- Dashboard updated
- Email notification sent

---

## 2️⃣ Suricata IDS Alert

### Purpose

Detect network reconnaissance and intrusion attempts.

### Data Source

- Suricata IDS

Examples include:

- Nmap Scan
- Port Scan
- Reconnaissance Activity

### Alert Action

- Dashboard updated
- Email notification sent

---

## 3️⃣ High Risk Score Alert

### Purpose

Notify analysts when the calculated Risk Score exceeds the configured threshold.

The Risk Score is derived from:

- Failed Login Attempts
- IDS Alerts
- Sysmon Activity
- Authentication Failures

When the threshold is exceeded:

- Email notification sent
- SOC investigation initiated

---

# 📨 Email Workflow

The alert lifecycle follows the workflow below.

```
Security Event

        │

        ▼

Detection Rule

        │

        ▼

Splunk Search

        │

        ▼

Trigger Condition Met

        │

        ▼

Email Alert

        │

        ▼

SOC Analyst
```

This ensures important events are immediately delivered to the analyst.

---

# ⚔️ Attack Validation

The alerting system was validated using controlled attacks.

---

## Windows Brute Force

### Attack Tool

Hydra

### Attack Flow

```
Hydra

↓

Windows Endpoint

↓

Windows Security Logs

↓

Splunk

↓

Detection Rule

↓

Dashboard Updated

↓

Email Sent
```

### Expected Result

✔ Failed Login Events Generated

✔ Dashboard Updated

✔ Email Received

---

## Ubuntu Nmap Scan

### Attack Tool

Nmap

### Attack Flow

```
Nmap

↓

Ubuntu

↓

Suricata IDS

↓

Splunk

↓

Detection Rule

↓

Dashboard Updated

↓

Email Sent
```

### Expected Result

✔ IDS Alert Generated

✔ Dashboard Updated

✔ Email Received

---

# 📧 Email Contents

Each alert email contains relevant security information to assist analysts.

Typical fields include:

- Alert Name
- Detection Time
- Hostname
- Source IP
- Destination IP
- Severity
- Event Details
- Trigger Reason

This enables analysts to begin investigating immediately without opening Splunk.

---

# 💡 Why Email Alerting Matters

A dashboard is effective only when someone is actively monitoring it.

In enterprise SOC environments, analysts often manage thousands of events every day. Automated alerting ensures that high-priority incidents are immediately delivered to the responsible analyst, reducing the risk of missed detections.

Benefits include:

- Faster Incident Response
- Reduced Mean Time to Detect (MTTD)
- Reduced Mean Time to Respond (MTTR)
- Improved SOC Efficiency
- Continuous Monitoring
- Faster Threat Investigation

Email alerting is one of the core capabilities of modern SIEM platforms and plays a critical role in operational security.

---

# 🛠 Future Improvements

Future enhancements include:

- Microsoft Teams Notifications
- Slack Integration
- SMS Alerts
- SOAR Automation
- ServiceNow Ticket Creation
- Risk-Based Alerting
- Multi-Stage Correlation Alerts
- Threat Intelligence Triggered Alerts

---

# 📸 Screenshots

Add the following screenshots:

- SMTP Configuration
- Alert Rule Configuration
- Triggered Alert
- Email Received
- Dashboard After Alert
- Splunk Search Results

---

# 📚 Related Documentation

- README.md
- Installation.md
- Dashboard-Setup.md
- Attack-Simulation.md
- Splunk-Dashboard-Claude-Skill.md
- Troubleshooting.md