# 📊 Splunk Dashboard Studio Guide

This guide explains how to create, configure, and customize the **SOC Dashboard** using **Splunk Dashboard Studio**.

Dashboard Studio is Splunk's modern visualization framework that enables the creation of highly interactive and customizable dashboards. In this project, it serves as the primary interface for monitoring security events, investigating incidents, and visualizing threat intelligence.

---

# 🎯 Objectives

The Dashboard Studio implementation in this project is designed to:

- Monitor security events in real time
- Visualize Windows and Linux logs
- Display Sysmon telemetry
- Monitor Suricata IDS alerts
- Support threat hunting
- Display Security KPIs
- Trigger analyst investigations
- Improve SOC visibility

---

# 🏗 Dashboard Architecture

```
Windows Endpoint
(Security + Sysmon)
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

Ubuntu + Suricata IDS

        │
        ▼

Dashboard Studio

        │
        ▼

SOC Analyst
```

---

# 📋 Dashboard Layout

The dashboard is divided into multiple logical sections.

```
┌──────────────────────────────────────┐
│ Executive KPIs                       │
├──────────────────────────────────────┤
│ Threat Analytics                     │
├──────────────────────────────────────┤
│ Threat Hunting                       │
├──────────────────────────────────────┤
│ Network & IDS Monitoring             │
├──────────────────────────────────────┤
│ MITRE ATT&CK Mapping                 │
├──────────────────────────────────────┤
│ Live Investigation Panel             │
└──────────────────────────────────────┘
```

This layout mirrors the workflow used by Security Operations Center (SOC) analysts.

---

# 📈 Executive KPIs

The KPI section provides an overview of the environment.

Example metrics include:

- Total Security Events
- Failed Login Attempts
- Critical IDS Alerts
- Active Hosts
- Risk Score
- Forwarder Health

Purpose:

Allow analysts to quickly assess the overall security posture.

---

# 📊 Threat Analytics

The Threat Analytics section visualizes trends over time.

Includes:

- Event Timeline
- Alert Timeline
- Top Event Codes
- Top Source IPs
- Top Destination IPs
- Event Distribution

Purpose:

Identify spikes, anomalies, and attack patterns.

---

# 🔍 Threat Hunting

This section provides visibility into endpoint activity.

### Windows

- Process Creation
- Network Connections
- DNS Queries
- File Creation
- Registry Events

### Linux

- Authentication Events
- SSH Activity
- Sudo Usage
- Kernel Logs

Purpose:

Support proactive threat hunting and investigation.

---

# 🛡 Suricata IDS Monitoring

The IDS section focuses on network-based detections.

Displays:

- Total IDS Alerts
- Alert Severity
- Top Signatures
- Top Attack Sources
- Protocol Distribution

Purpose:

Monitor suspicious network activity in real time.

---

# 🎯 MITRE ATT&CK Mapping

Detected events are categorized using the MITRE ATT&CK framework.

Examples:

| Technique | ID |
|------------|----|
| Brute Force | T1110 |
| Active Scanning | T1595 |
| Network Service Discovery | T1046 |

Purpose:

Help analysts understand attacker tactics and techniques.

---

# 🌍 Geo-IP Visualization

Displays the geographic location of detected IP addresses.

Shows:

- Source Countries
- Destination Countries
- Connection Distribution

Purpose:

Identify unexpected or suspicious geographic activity.

---

# 📌 Risk Score

The dashboard calculates a custom security risk score using:

- Failed Login Attempts
- IDS Alerts
- Sysmon Activity
- Authentication Failures

Purpose:

Provide a high-level indicator of the current security posture.

---

# 🔎 Live Investigation Panel

The investigation panel displays raw security events for rapid analysis.

Typical fields include:

- Timestamp
- Host
- Source IP
- Destination IP
- Event Type
- Severity
- Event Details

Purpose:

Enable analysts to pivot from dashboards into detailed investigations.

---

# 🎨 Dashboard Design Principles

The dashboard follows modern SOC design standards.

Key principles include:

- Minimal visual clutter
- Analyst-focused layout
- Consistent color scheme
- Clear KPI hierarchy
- Interactive filtering
- Responsive layout
- Fast visual interpretation

---

# ⚙ Dashboard Studio Features

The dashboard leverages Dashboard Studio capabilities such as:

- Interactive Charts
- Single Value Visualizations
- Tables
- Pie Charts
- Bar Charts
- Area Charts
- Line Charts
- Markdown Panels
- Dynamic Filters

---

# 🚀 Creating the Dashboard

## Step 1

Open Splunk.

```
Apps

↓

Dashboard Studio
```

---

## Step 2

Create a new dashboard.

Choose:

```
Blank Dashboard
```

---

## Step 3

Configure the global settings.

- Theme
- Time Picker
- Default Time Range
- Dashboard Layout

---

## Step 4

Add visualizations.

Examples:

- Single Value
- Table
- Line Chart
- Area Chart
- Bar Chart
- Pie Chart
- Markdown

---

## Step 5

Assign SPL queries to each visualization.

Example:

```spl
index=* sourcetype="WinEventLog:Security"
| stats count by EventCode
```

---

## Step 6

Arrange panels according to the SOC layout.

---

## Step 7

Save the dashboard.

---

# 📸 Dashboard Screenshots

Include screenshots for:

- Dashboard Overview
- KPI Row
- Threat Timeline
- Sysmon Monitoring
- Suricata IDS
- MITRE ATT&CK Mapping
- Geo-IP Panel
- Live Investigation
- Email Alert Integration

---

# 🤖 AI-Assisted Dashboard Development

This dashboard was designed with the assistance of a custom **Claude Skill** developed specifically for Splunk Dashboard Studio.

The AI framework helps generate:

- Dashboard architecture
- JSON layouts
- Visualization recommendations
- SPL optimization
- KPI placement
- Threat hunting workflows
- SOC design best practices

For more information, see:

> **Splunk-Dashboard-Claude-Skill.md**

---

# 🚀 Future Enhancements

Planned improvements include:

- Glassmorphism UI
- Drilldown Workflows
- Dark/Light Theme Support
- Dynamic Risk Scoring
- Threat Intelligence Enrichment
- Executive Dashboard
- SOAR Integration
- Sigma Rule Panels
- UEBA Visualizations

---

# 📚 Related Documentation

- README.md
- Dashboard.md
- Installation.md
- Email-Alerting.md
- Attack-Simulation.md
- Splunk-Dashboard-Claude-Skill.md
- Troubleshooting.md
