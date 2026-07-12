# Changelog

All notable changes to this project will be documented in this file.

The format is based on **Keep a Changelog** and this project follows **Semantic Versioning (SemVer)**.

---

## [1.0.0] - 2026-07-12

### 🎉 Initial Public Release

The first stable release of the **Splunk SOC Home Lab** project.

---

## ✨ Added

### SOC Infrastructure

- Splunk Enterprise Server
- Windows Endpoint with Splunk Universal Forwarder
- Ubuntu Endpoint with Splunk Universal Forwarder
- Kali Linux Attacker Machine

---

### Log Collection

#### Windows

- Security Event Logs
- System Logs
- Application Logs
- Sysmon Operational Logs

#### Linux

- Syslog
- Authentication Logs
- Kernel Logs

---

### Security Monitoring

- Sysmon Integration
- Suricata IDS Integration
- Centralized Log Collection
- Real-time Event Monitoring

---

### Dashboard Studio

Designed and implemented an advanced SOC Dashboard using Splunk Dashboard Studio.

Features include:

- Executive Security KPIs
- Threat Timeline
- Risk Score
- Top Source IPs
- Top Destination IPs
- Event Distribution
- MITRE ATT&CK Mapping
- Threat Hunting Panels
- Sysmon Monitoring
- Linux Authentication Monitoring
- Suricata IDS Monitoring
- Geo-IP Visualization
- Live Investigation Panel

---

### AI-Assisted Dashboard Development

Developed a custom **Claude Skill** for Splunk Dashboard Studio.

Capabilities include:

- Dashboard Planning
- Dashboard Studio JSON Generation
- SPL Optimization
- Visualization Selection
- Dashboard Architecture
- KPI Design
- Threat Hunting Workflow
- Security Dashboard Best Practices

---

### Detection Engineering

Implemented detections for:

- Windows Brute Force Attacks
- Network Reconnaissance
- Suricata IDS Alerts
- Failed Login Monitoring
- Risk Score Monitoring

---

### Email Alerting

Configured Splunk Email Alerting using Gmail SMTP.

Implemented alerts for:

- Windows Brute Force Detection
- Suricata IDS Detection
- High Risk Score

---

### Attack Validation

Validated the complete SOC pipeline using controlled attack simulations.

#### Windows

- Hydra Brute Force Attack

#### Ubuntu

- Nmap Network Reconnaissance

Verified:

- Event Generation
- Log Collection
- Dashboard Updates
- Detection Rules
- Email Alerts

---

### Documentation

Added complete project documentation.

- README
- Installation Guide
- Dashboard Setup Guide
- Email Alerting Guide
- Attack Simulation Guide
- Troubleshooting Guide
- Claude Skill Documentation
- Future Roadmap

---

### Repository

Initial GitHub repository structure created.

```
splunk-soc-home-lab/

├── README.md
├── LICENSE
├── CHANGELOG.md
├── Splunk-Dashboard-Claude-Skill.md

├── architecture/
├── dashboard/
├── alerts/
├── docs/
└── screenshots/
```

---

## 📈 Learning Outcomes

This project strengthened practical experience in:

- SIEM Engineering
- SOC Operations
- Detection Engineering
- Threat Hunting
- Incident Response
- Windows Security Monitoring
- Linux Security Monitoring
- Splunk Enterprise
- Dashboard Studio
- Sysmon
- Suricata IDS
- Email Alerting
- MITRE ATT&CK
- AI-Assisted Dashboard Engineering

---

## 🚀 Planned for Version 1.1.0

- Wazuh Integration
- Sigma Rule Detection
- PowerShell Logging
- Threat Intelligence Integration
- Advanced Correlation Searches
- Risk-Based Alerting
- SOAR Integration
- Machine Learning Analytics
- Executive SOC Dashboard
- Additional Detection Rules
- Enhanced Threat Hunting Panels
- Improved Dashboard Performance

---

## Version History

| Version | Release Date | Description |
|----------|--------------|-------------|
| **1.0.0** | 2026-07-12 | Initial public release of the Splunk SOC Home Lab |