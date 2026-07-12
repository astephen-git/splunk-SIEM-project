# 🤖 How to Use the Claude Skill

This guide explains how to use the **Splunk Dashboard Claude Skill** included in this repository.

The skill is designed to help security engineers, SOC analysts, Splunk developers, and dashboard designers generate **professional Splunk Dashboard Studio dashboards** using natural language.

Instead of manually designing every panel and writing Dashboard Studio JSON from scratch, the Claude Skill acts as an AI-powered dashboard architect that follows SOC design principles and Splunk best practices.

---

# 📌 What is the Claude Skill?

The Claude Skill is a specialized prompt engineered specifically for **Splunk Dashboard Studio**.

It understands:

- Splunk Dashboard Studio JSON
- Dashboard architecture
- Security dashboard design
- KPI placement
- Visualization selection
- Threat hunting workflows
- MITRE ATT&CK mapping
- SPL optimization
- Security UX principles

The goal is to transform user requirements into a production-ready dashboard design.

---

# 🎯 Supported Dashboard Types

The skill can generate dashboards for:

- Security Operations Center (SOC)
- Threat Hunting
- Blue Team Monitoring
- Incident Response
- Windows Security
- Linux Security
- Sysmon Monitoring
- Suricata IDS
- Firewall Monitoring
- Network Monitoring
- Vulnerability Management
- Compliance Reporting
- Executive Security Dashboards
- Operational Dashboards

---

# 🚀 Getting Started

## Step 1

Copy the contents of:

```
Splunk-Dashboard-Claude-Skill.md
```

---

## Step 2

Open Claude AI.

---

## Step 3

Create a new Project (recommended).

---

## Step 4

Paste the skill into the Project Knowledge or System Prompt.

---

## Step 5

Start describing the dashboard you want.

Example:

```
Build a professional SOC dashboard using Dashboard Studio.

Environment:

- Splunk Enterprise

Windows Endpoint

- Windows Security Logs
- Sysmon

Ubuntu Endpoint

- Syslog
- Authentication Logs
- Suricata IDS

Requirements:

• Executive KPI row

• Threat Timeline

• Risk Score

• MITRE ATT&CK Mapping

• Threat Hunting

• Geo-IP

• Live Investigation

Use a modern dark theme with glassmorphism.
```

The skill will generate a structured dashboard design based on these requirements.

---

# 📝 Example Prompts

## Example 1

```
Design a SOC dashboard for Windows event monitoring.

Include:

- Failed Logins
- Successful Logins
- Privileged Logons
- Account Creation
- Risk Score
```

---

## Example 2

```
Build a Threat Hunting dashboard using Sysmon.

Include:

- Process Creation
- DNS Queries
- Network Connections
- File Creation
- Registry Activity
```

---

## Example 3

```
Create a Suricata IDS monitoring dashboard.

Include:

- Alert Timeline
- Top Attackers
- Top Destinations
- Alert Severity
- Alert Categories
```

---

## Example 4

```
Generate an Executive Security Dashboard.

Include:

- Security KPIs
- Risk Score
- MITRE ATT&CK Coverage
- Top Threats
- Active Hosts
```

---

# 🏗 Recommended Workflow

```
Collect Requirements

        │

        ▼

Claude Skill

        │

        ▼

Dashboard Architecture

        │

        ▼

Generate SPL Queries

        │

        ▼

Generate Dashboard Studio JSON

        │

        ▼

Import into Splunk

        │

        ▼

Validate Dashboard

        │

        ▼

Deploy
```

---

# 💡 Best Practices

For the best results:

✅ Clearly describe your environment.

✅ List your data sources.

✅ Mention all indexes.

✅ Specify required visualizations.

✅ Mention the dashboard theme.

✅ Include analyst workflow requirements.

✅ Specify the investigation process.

The more detailed your prompt, the better the generated dashboard.

---

# 📊 Example Environment

```
Splunk Enterprise

Windows Endpoint

- Security Logs

- Sysmon

Ubuntu Endpoint

- Syslog

- Authentication Logs

- Suricata IDS

Kali Linux

Attack Simulation
```

---

# 🎨 Dashboard Design Recommendations

The Claude Skill follows these design principles:

- Executive KPIs at the top
- Threat analytics in the middle
- Investigation panels at the bottom
- Consistent color palette
- Minimal visual clutter
- SOC analyst focused layout
- Fast visual interpretation
- Interactive filtering

---

# ⚠ Limitations

The Claude Skill generates dashboard designs based on the information provided.

Before deployment:

- Verify SPL queries.
- Confirm field names.
- Validate indexes.
- Test visualizations.
- Adjust layouts if required.

Some environments may require customization depending on installed Splunk apps, data models, and field extractions.

---

# 🤝 Contributing

Suggestions and improvements are welcome.

If you have ideas for improving the Claude Skill, feel free to open an issue or submit a pull request.

---

# 📚 Related Documentation

- README.md
- Splunk-Dashboard-Claude-Skill.md
- Dashboard-Setup.md
- Installation.md
- Email-Alerting.md
- Attack-Simulation.md
- Troubleshooting.md