# 📊 Dashboard Setup Guide

This document explains the design, implementation, and workflow of the **Splunk Dashboard Studio** dashboard built for this project.

The dashboard is designed to provide a **real-time Security Operations Center (SOC) view** by combining telemetry from Windows, Linux, Sysmon, and Suricata IDS into a single interactive interface.

Unlike a traditional dashboard that only displays logs, this dashboard focuses on **security monitoring, threat detection, threat hunting, and incident investigation**.

---

# 🎯 Dashboard Objectives

The dashboard was designed with the following goals:

- Provide real-time visibility into the environment
- Reduce investigation time
- Identify suspicious activities quickly
- Display critical security KPIs
- Support SOC analysts during investigations
- Visualize endpoint and network telemetry
- Monitor IDS alerts
- Map detections to MITRE ATT&CK
- Trigger investigations through visual indicators

---

# 🏗 Dashboard Architecture

```
                Windows Endpoint
           Security Logs + Sysmon
                     │
                     │
                     ▼

             Splunk Universal Forwarder
                     │

                     ▼

               Splunk Enterprise
                     ▲
                     │

             Splunk Universal Forwarder
                     ▲
                     │

       Ubuntu Endpoint + Suricata IDS

                     │
                     ▼

          Dashboard Studio (SOC Dashboard)

                     │
                     ▼

           SOC Analyst Investigation
```

---

# 🎨 Dashboard Design Philosophy

The dashboard follows standard SOC design principles.

The layout is divided into multiple sections based on analyst workflow.

```
Top
↓

Executive KPIs

↓

Threat Analytics

↓

Threat Hunting

↓

Network Monitoring

↓

MITRE ATT&CK

↓

Live Investigation

↓

Raw Events
```

This layout allows analysts to understand the overall security posture before diving into detailed investigations.

---

# 📈 Executive KPI Section

The first row provides a quick overview of the environment.

### Widgets

- Total Security Events
- Critical Alerts
- Failed Logins
- Active Hosts
- Risk Score
- Forwarder Health

Purpose:

Provide instant awareness of the current environment.

---

# 📊 Threat Analytics

This section visualizes security activity over time.

Panels include:

- Event Timeline
- Alert Trend
- Top Event Codes
- Top Source IPs
- Top Destination IPs
- Top Alert Signatures

Purpose:

Help analysts identify unusual activity and attack patterns.

---

# 🛡 Threat Hunting

The dashboard contains dedicated threat hunting panels.

## Windows Threat Hunting

Monitored using Sysmon.

Panels include:

- Process Creation
- Parent/Child Processes
- Network Connections
- File Creation
- DNS Queries
- Registry Activity

Purpose:

Detect suspicious endpoint behavior.

---

## Linux Monitoring

Panels include:

- Authentication Logs
- SSH Activity
- Sudo Commands
- Kernel Events

Purpose:

Monitor Linux authentication and privilege escalation.

---

## Suricata IDS Monitoring

Suricata events are visualized separately.

Panels include:

- IDS Alerts
- Alert Severity
- Alert Categories
- Top Attackers
- Protocol Distribution

Purpose:

Provide network intrusion visibility.

---

# 🌍 Network Visibility

The dashboard includes network monitoring panels.

Features:

- Top Source IPs
- Top Destination IPs
- Geo-IP Visualization
- Connection Trends

Purpose:

Identify suspicious network communication.

---

# 🎯 MITRE ATT&CK Mapping

Detected activities are mapped to the MITRE ATT&CK framework.

Examples include:

- Brute Force
- Discovery
- Command Execution
- Persistence
- Privilege Escalation
- Credential Access

Purpose:

Help analysts understand attacker techniques.

---

# 📌 Risk Score

A custom Risk Score is calculated from multiple data sources.

Inputs include:

- Failed Login Attempts
- Critical IDS Alerts
- Sysmon Activity
- Authentication Failures

Purpose:

Provide a single indicator of overall security health.

---

# 🔎 Live Investigation Panel

The investigation panel displays live security events.

Fields include:

- Timestamp
- Host
- Source
- Sourcetype
- Severity
- Event Details

Purpose:

Allow analysts to investigate events without switching dashboards.

---

# 🔄 Dashboard Filters

Global filters are available across the dashboard.

Filters include:

- Time Range
- Host
- Index
- Sourcetype

Changing a filter updates every panel automatically.

---

# 🚨 Email Alert Integration

The dashboard works together with Splunk Email Alerting.

When critical detections occur:

```
Detection

↓

Dashboard Update

↓

Email Alert

↓

SOC Investigation
```

This ensures analysts are notified immediately.

---

# ⚔ Attack Demonstration

The dashboard was validated using controlled attacks.

## Windows Brute Force

Attack Tool:

- Hydra

Flow:

```
Hydra

↓

Windows Endpoint

↓

Windows Security Logs

↓

Splunk

↓

Dashboard

↓

Email Alert
```

Dashboard Response:

- Failed Login Counter Increased
- Risk Score Increased
- Timeline Updated
- Email Alert Sent

---

## Ubuntu Network Scan

Attack Tool:

- Nmap

Flow:

```
Nmap

↓

Ubuntu

↓

Suricata IDS

↓

Splunk

↓

Dashboard

↓

Email Alert
```

Dashboard Response:

- IDS Alert Generated
- Timeline Updated
- Source IP Displayed
- Email Alert Sent

---

# 🎨 Dashboard Technologies

The dashboard uses:

- Splunk Dashboard Studio
- SPL (Search Processing Language)
- Windows Event Logs
- Sysmon
- Suricata IDS
- MITRE ATT&CK
- Geo-IP
- Email Alerting

---

# 🤖 AI-Assisted Dashboard Development

A custom **Claude Skill** was created specifically for this project.

The skill assists in:

- Dashboard planning
- JSON generation
- Dashboard Studio architecture
- SPL optimization
- Panel placement
- Visualization selection
- Threat hunting workflow
- Dashboard UX

This significantly reduced dashboard development time while maintaining a professional SOC layout.

For more information, see:

> **Splunk-Dashboard-Claude-Skill.md**

---

# 📸 Dashboard Screenshots

Add screenshots of the following sections here:

- Dashboard Overview
- KPI Section
- Threat Timeline
- Sysmon Panel
- Suricata Panel
- MITRE ATT&CK Mapping
- Geo-IP Visualization
- Live Investigation
- Email Alert
- Attack Demonstration

---

# 🚀 Future Enhancements

Planned improvements include:

- Wazuh Integration
- Sigma Rule Correlation
- Threat Intelligence Feeds
- SOAR Automation
- PowerShell Logging
- Machine Learning Detection
- UEBA
- Risk-Based Alerting
- Executive Dashboard
- Dark Glassmorphism Dashboard Theme

---

# 📚 Related Documentation

- README.md
- Installation.md
- Email-Alerting.md
- Attack-Simulation.md
- Splunk-Dashboard-Claude-Skill.md
- Troubleshooting.md