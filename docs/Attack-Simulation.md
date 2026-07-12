# ⚔️ Attack Simulation Guide

This document explains how the **Splunk SOC Home Lab** was validated using controlled attack simulations.

The purpose of these simulations is to verify that the entire SOC pipeline—from attack generation to detection, visualization, and alerting—is functioning correctly.

The attacks were performed **only within an isolated lab environment** for educational and defensive security purposes.

---

# 🎯 Objectives

The attack simulations were designed to validate:

- Windows Event Log Collection
- Linux Log Collection
- Sysmon Monitoring
- Suricata IDS Detection
- Splunk Log Ingestion
- Dashboard Updates
- Email Alerting
- Incident Investigation Workflow

---

# 🖥️ Lab Environment

| Machine | Purpose |
|----------|----------|
| Splunk Enterprise Server | SIEM Platform |
| Windows Endpoint | Target Machine |
| Ubuntu Endpoint | Linux Target + Suricata IDS |
| Kali Linux | Attacker Machine |

---

# 🔄 Attack Workflow

```
           Kali Linux
                │
                ▼
      Attack Simulation
                │
      ┌─────────┴─────────┐
      ▼                   ▼
 Windows Endpoint     Ubuntu Endpoint
      │                   │
      ▼                   ▼
Windows Logs        Suricata IDS
      │                   │
      └─────────┬─────────┘
                ▼
      Splunk Universal Forwarder
                │
                ▼
       Splunk Enterprise
                │
      ┌─────────┼──────────┐
      ▼         ▼          ▼
 Dashboard   Detection   Email Alert
                │
                ▼
         SOC Investigation
```

---

# 🔴 Attack Scenario 1 – Windows Brute Force Attack

## Objective

Simulate a password brute-force attack against a Windows system.

---

## Attacker Machine

**Operating System**

- Kali Linux

**Tool Used**

- Hydra

---

## Target

- Windows Endpoint

---

## Attack Process

A brute-force attack was launched from the Kali Linux machine against the Windows endpoint.

The attack intentionally generated multiple failed authentication attempts to trigger Windows Security Event logging.

---

## Detection Pipeline

```
Hydra

↓

Windows Login Attempt

↓

Windows Security Event 4625

↓

Splunk Universal Forwarder

↓

Splunk Enterprise

↓

Detection Rule

↓

SOC Dashboard Updated

↓

Email Alert Sent
```

---

## Splunk Logs Generated

Examples include:

- Event ID 4625 – Failed Login
- Authentication Failure
- Source Host
- Target User
- Timestamp

---

## Dashboard Response

The SOC Dashboard automatically updated to display:

- Increased Failed Login Counter
- Risk Score Increase
- Threat Timeline Update
- Live Investigation Event
- Windows Security Events

---

## Alert Response

The configured email alert was triggered automatically.

The analyst received a notification containing:

- Alert Name
- Host
- Username
- Event Time
- Trigger Condition

---

# 🔵 Attack Scenario 2 – Ubuntu Network Reconnaissance

## Objective

Validate network intrusion detection using Suricata IDS.

---

## Attacker Machine

- Kali Linux

---

## Tool Used

- Nmap

---

## Target

- Ubuntu Endpoint

---

## Attack Process

A network scan was launched against the Ubuntu machine.

Suricata IDS continuously monitored network traffic and detected the reconnaissance activity.

---

## Detection Pipeline

```
Nmap

↓

Ubuntu Network

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

SOC Dashboard Updated

↓

Email Alert Sent
```

---

## Suricata Detection

Suricata generated alerts such as:

- Nmap Scan Detected
- Port Scan
- Network Reconnaissance
- Suspicious Traffic

---

## Dashboard Response

The dashboard displayed:

- IDS Alert Count
- Threat Timeline Update
- Source IP
- Destination IP
- Alert Severity
- Alert Signature
- Risk Score Increase

---

## Alert Response

Splunk automatically generated an email notification containing:

- Alert Name
- Source IP
- Destination IP
- Alert Signature
- Severity
- Detection Time

---

# 📊 Detection Summary

| Attack | Detection | Dashboard | Email |
|----------|-----------|-----------|-------|
| Windows Brute Force | ✅ | ✅ | ✅ |
| Ubuntu Nmap Scan | ✅ | ✅ | ✅ |

---

# 🛡️ Security Components Validated

The attack simulations confirmed the successful operation of:

- Windows Event Logging
- Linux System Logging
- Sysmon Monitoring
- Suricata IDS
- Splunk Universal Forwarder
- Splunk Enterprise
- Dashboard Studio
- Detection Rules
- Email Alerting

---

# 💡 Key Learning Outcomes

This project demonstrates the complete lifecycle of a security incident within a SOC environment.

From attack generation to analyst notification, every stage of the detection pipeline was validated using real telemetry.

The simulations provided practical experience with:

- Threat Detection
- Log Analysis
- SIEM Engineering
- Detection Engineering
- Dashboard Development
- Incident Monitoring
- Security Alerting
- Threat Hunting

---

# 🚀 Future Attack Simulations

Future versions of the lab will include additional attack scenarios, including:

- Password Spraying
- SSH Brute Force
- Reverse Shell Detection
- PowerShell Attacks
- Malware Simulation
- File Integrity Monitoring
- Persistence Techniques
- Privilege Escalation
- Credential Dumping
- Lateral Movement
- Command and Control (C2)
- Data Exfiltration

---

# 📸 Screenshots

Include screenshots of:

- Hydra Brute Force Execution
- Windows Event Viewer
- Splunk Search Results
- Dashboard During Brute Force
- Email Alert (Windows)
- Nmap Scan
- Suricata Detection
- Splunk IDS Events
- Dashboard During Nmap Scan
- Email Alert (Suricata)

---

# 📚 Related Documentation

- README.md
- Installation.md
- Dashboard-Setup.md
- Email-Alerting.md
- Splunk-Dashboard-Claude-Skill.md
- Troubleshooting.md