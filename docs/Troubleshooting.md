# 🛠️ Troubleshooting Guide

This document contains common issues encountered while building the **Splunk SOC Home Lab** and their solutions.

Most of these problems were experienced during the development of this project and documented to help others reproduce the lab successfully.

---

# 📋 Troubleshooting Categories

- Splunk Enterprise
- Universal Forwarder
- Windows Event Logs
- Sysmon
- Ubuntu Logs
- Suricata IDS
- Dashboard Studio
- Email Alerting
- Attack Simulation

---

# 🖥️ Splunk Enterprise Issues

## Issue 1 — Splunk Web Not Accessible

### Symptoms

- Unable to access the Splunk Web interface.
- Browser displays "This site can't be reached."

### Possible Causes

- Splunk service is not running.
- Firewall blocks port 8000.
- Incorrect IP address.

### Solution

Verify the Splunk service is running.

On Windows:

```
services.msc
```

Restart:

```
Splunkd
```

Verify access:

```
https://<Splunk-IP>:8000
```

---

## Issue 2 — Universal Forwarder Not Connected

### Symptoms

- No events appear in Splunk.
- Forwarder status is inactive.

### Possible Causes

- Incorrect server IP.
- Receiving port disabled.
- Firewall blocking port 9997.

### Solution

Verify receiving is enabled.

```
Settings

↓

Forwarding and Receiving

↓

Configure Receiving

↓

9997
```

Restart the Universal Forwarder.

Check the connection status.

---

# 💻 Windows Event Log Issues

## Issue 3 — Windows Logs Not Appearing

### Symptoms

No Security, System, or Application logs appear.

### Solution

Verify:

```
inputs.conf
```

contains:

- Security
- System
- Application

Restart the Universal Forwarder.

---

## Issue 4 — Sysmon Events Missing

### Symptoms

Sysmon Event IDs do not appear.

### Possible Causes

- Sysmon not installed.
- Incorrect configuration.
- Sysmon service stopped.

### Solution

Verify installation:

```
sysmon64.exe -i sysmonconfig.xml
```

Open Event Viewer.

Navigate to:

```
Applications and Services Logs

↓

Microsoft

↓

Windows

↓

Sysmon

↓

Operational
```

Confirm events such as:

- Event ID 1
- Event ID 3
- Event ID 11
- Event ID 22

are being generated.

---

# 🐧 Ubuntu Issues

## Issue 5 — Linux Logs Missing

### Symptoms

No Ubuntu events appear.

### Solution

Verify monitoring paths:

```
/var/log/syslog

/var/log/auth.log

/var/log/kern.log
```

Restart the Universal Forwarder.

---

# 🛡️ Suricata IDS Issues

## Issue 6 — Suricata Alerts Missing

### Symptoms

Nmap scans do not generate alerts.

### Possible Causes

- Suricata service stopped.
- Incorrect HOME_NET.
- eve.json disabled.

### Solution

Verify service:

```
sudo systemctl status suricata
```

Check:

```
suricata.yaml
```

Ensure:

```
eve.json
```

is enabled.

Restart Suricata.

---

## Issue 7 — eve.json Not Forwarded

### Symptoms

Suricata generates alerts locally but not in Splunk.

### Solution

Verify Universal Forwarder monitors:

```
/var/log/suricata/eve.json
```

Restart the Universal Forwarder.

---

# 📊 Dashboard Studio Issues

## Issue 8 — Dashboard Panel Empty

### Symptoms

Visualization loads but shows no data.

### Possible Causes

- Incorrect SPL query.
- Wrong index.
- Wrong time range.

### Solution

Test the SPL query in Search first.

Confirm:

- Correct index
- Correct sourcetype
- Correct field names

---

## Issue 9 — Dashboard Slow

### Symptoms

Panels load slowly.

### Solution

Optimize SPL.

Prefer:

```
tstats
```

instead of:

```
stats
```

Reduce unnecessary searches.

Limit returned fields.

---

# 📧 Email Alerting Issues

## Issue 10 — Email Not Sent

### Symptoms

Alert triggers but no email is received.

### Possible Causes

- SMTP misconfiguration.
- Invalid credentials.
- Gmail security restrictions.

### Solution

Verify:

- SMTP Server
- Port
- TLS
- Username
- App Password

Send a test email from Splunk.

---

## Issue 11 — Alert Never Triggers

### Symptoms

Dashboard updates but email is never sent.

### Solution

Check:

- Alert schedule
- Trigger condition
- Search results
- Time range

Ensure the search actually returns events.

---

# ⚔️ Attack Simulation Issues

## Issue 12 — Hydra Attack Not Logged

### Symptoms

Hydra runs but Event ID 4625 is missing.

### Solution

Verify:

- Windows Firewall
- RDP Enabled
- Correct Credentials
- Security Auditing Enabled

---

## Issue 13 — Nmap Not Detected

### Symptoms

Nmap completes successfully but Suricata detects nothing.

### Solution

Verify:

- Suricata running
- Correct network interface
- HOME_NET configured
- Detection rules enabled

---

# 🔍 Log Verification

Always verify events are present before troubleshooting dashboards.

Examples:

Windows:

```
index=* sourcetype="WinEventLog:Security"
```

Linux:

```
index=* sourcetype=syslog
```

Suricata:

```
index=* sourcetype=suricata
```

Sysmon:

```
index=* source="XmlWinEventLog:Microsoft-Windows-Sysmon/Operational"
```

---

# ✅ Health Checklist

Confirm the following:

- Splunk Enterprise running
- Receiving port enabled
- Universal Forwarders connected
- Windows logs visible
- Sysmon logs visible
- Ubuntu logs visible
- Suricata alerts visible
- Dashboard operational
- Email alerts working
- Attack simulation successful

---

# 🚀 Best Practices

- Test SPL searches before adding them to dashboards.
- Verify data ingestion before creating alerts.
- Use descriptive dashboard titles.
- Keep detection rules simple and well documented.
- Regularly update Sysmon and Suricata configurations.
- Monitor Universal Forwarder status.
- Document every configuration change.

---

# 📚 Related Documentation

- README.md
- Installation.md
- Dashboard-Setup.md
- Email-Alerting.md
- Attack-Simulation.md
- Splunk-Dashboard-Claude-Skill.md