# 🛠️ Installation Guide

This guide explains how to recreate the complete **Splunk SOC Home Lab** from scratch.

The environment consists of four virtual/physical machines connected within the same network.

---

# 📋 Lab Environment

| Machine | Operating System | Purpose |
|----------|------------------|----------|
| Splunk Server | Windows 11 | SIEM, Dashboard, Alerting |
| Windows Endpoint | Windows 10 | Endpoint Monitoring |
| Ubuntu Endpoint | Ubuntu 22.04 | Linux Monitoring & Suricata IDS |
| Attacker | Kali Linux | Attack Simulation |

---

# 📦 Software Requirements

## Splunk Server

Install:

- Splunk Enterprise
- Splunk Dashboard Studio
- Splunk Universal Forwarder (optional)
- Gmail SMTP (for Email Alerting)

Minimum Recommended:

- 8 GB RAM
- 4 CPU Cores
- 100 GB Storage

---

## Windows Endpoint

Install:

- Splunk Universal Forwarder
- Sysmon
- Sysmon Configuration

Logs Collected:

- Security
- System
- Application
- Sysmon Operational

---

## Ubuntu Endpoint

Install:

- Splunk Universal Forwarder
- Suricata IDS

Logs Collected:

- Syslog
- Auth Logs
- Kernel Logs
- Suricata Alerts

---

## Kali Linux

Install:

- Hydra
- Nmap

Used for attack simulations.

---

# 🌐 Network Configuration

All systems must communicate over the same network.

Example:

| Machine | IP Address |
|----------|------------|
| Splunk Server | 192.168.1.100 |
| Windows Endpoint | 192.168.1.101 |
| Ubuntu Endpoint | 192.168.1.102 |
| Kali Linux | 192.168.1.103 |

> Your IP addresses may differ.

---

# 📥 Install Splunk Enterprise

Download Splunk Enterprise from the official Splunk website.

Install using the default settings.

Access the web interface:

```
https://<Splunk-IP>:8000
```

Create the administrator account during setup.

---

# 📥 Install Splunk Universal Forwarder

Install the Splunk Universal Forwarder on both Windows and Ubuntu endpoints.

During installation configure:

```
Receiving Indexer

Server:
<Splunk-IP>:9997
```

---

# ⚙️ Configure Splunk Server

Enable receiving:

```
Settings

→ Forwarding and Receiving

→ Configure Receiving

→ Port 9997
```

Verify the receiver is active.

---

# 🪟 Configure Windows Log Collection

Edit:

```
inputs.conf
```

Enable:

```
Windows Security

Windows System

Windows Application

Sysmon
```

Restart the Universal Forwarder.

Verify events appear in Splunk.

---

# 🔍 Install Sysmon

Download Sysmon from Microsoft Sysinternals.

Install:

```
sysmon64.exe -accepteula -i sysmonconfig.xml
```

Verify:

```
Applications and Services Logs

Microsoft

Windows

Sysmon

Operational
```

Expected Event IDs:

- 1 Process Creation
- 3 Network Connections
- 11 File Creation
- 22 DNS Query

---

# 🐧 Configure Ubuntu Logs

Enable forwarding for:

```
/var/log/syslog

/var/log/auth.log

/var/log/kern.log
```

Restart the Universal Forwarder.

Verify events in Splunk.

---

# 🛡️ Install Suricata IDS

Install:

```
sudo apt update

sudo apt install suricata
```

Verify:

```
sudo systemctl status suricata
```

Enable:

```
eve.json
```

Configure the Universal Forwarder to monitor:

```
/var/log/suricata/eve.json
```

Restart the forwarder.

Verify IDS alerts appear in Splunk.

---

# 📊 Dashboard Studio

Create a new Dashboard Studio dashboard.

Configure:

- KPIs
- Risk Score
- Timeline
- MITRE ATT&CK
- Geo-IP
- Threat Hunting
- Live Investigation

Import dashboard JSON if available.

---

# 📧 Configure Email Alerting

Configure SMTP inside Splunk.

Recommended:

- Gmail App Password
- TLS Enabled

Test the configuration.

Create alerts for:

- Windows Brute Force
- Suricata IDS
- High Risk Score

Verify email delivery.

---

# ⚔️ Attack Simulation

## Windows Brute Force

From Kali Linux:

```
Hydra

↓

Windows Login

↓

Windows Security Logs

↓

Splunk

↓

Dashboard

↓

Email Alert
```

Expected Result:

- Failed Login Events

- Dashboard Updates

- Email Notification

---

## Ubuntu Nmap Scan

Run:

```
nmap <Ubuntu-IP>
```

Expected Flow:

```
Kali

↓

Ubuntu

↓

Suricata

↓

Splunk

↓

Dashboard

↓

Email Alert
```

Expected Result:

- Suricata Alert

- Dashboard Updates

- Email Notification

---

# ✅ Verification Checklist

Confirm the following before considering the installation complete.

- Splunk Enterprise running
- Universal Forwarders connected
- Windows logs received
- Sysmon logs received
- Linux logs received
- Suricata alerts received
- Dashboard operational
- Email alerting functional
- Attack simulation successful

---

# 🚀 Next Improvements

Future enhancements include:

- Wazuh Integration

- Sigma Rules

- Threat Intelligence

- SOAR Automation

- PowerShell Logging

- Detection Engineering

- Risk-Based Alerting

- Machine Learning

---

# 📚 Related Documentation

- README.md
- Dashboard.md
- Email-Alerting.md
- Attack-Simulation.md
- Splunk-Dashboard-Claude-Skill.md
- Troubleshooting.md