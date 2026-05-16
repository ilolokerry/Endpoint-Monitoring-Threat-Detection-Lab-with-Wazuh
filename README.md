
# 🔐 SOC Lab – Endpoint Monitoring & Threat Detection with Wazuh

## 📌 Project Overview

This project is a hands-on SOC (Security Operations Center) lab designed to simulate real-world security monitoring and threat detection operations using endpoint and network telemetry.

The lab focuses on detecting, analyzing, and investigating malicious activity across endpoint and network environments through SIEM monitoring, IDS/IPS detection, log analysis, and threat investigation workflows.

> 🚧 Status: In Progress

---

# 🧠 Objectives

- Build a practical SOC monitoring environment
- Monitor endpoint and network activity
- Detect malicious behavior and attack patterns
- Investigate security alerts and suspicious events
- Practice incident response and threat analysis workflows
- Simulate real-world blue team operations

---

# 🏗️ Lab Architecture

```text
                 ┌──────────────────────┐
                 │   Attacker VM        │
                 │ (Kali / Test System) │
                 └──────────┬───────────┘
                            │
                     Network Traffic
                            │
                ┌───────────▼───────────┐
                │  Suricata IDS/IPS     │
                │ Network Monitoring    │
                └───────────┬───────────┘
                            │
                     Suricata Logs
                            │
                ┌───────────▼───────────┐
                │      Wazuh SIEM       │
                │ Alerting & Analysis   │
                └───────┬─────────┬─────┘
                        │         │
              Endpoint Logs   Security Alerts
                        │
          ┌─────────────▼─────────────┐
          │ Windows / Linux Endpoints │
          │ Wazuh Agent + Sysmon      │
          └───────────────────────────┘
```
---

# ⚙️ Technologies & Concepts

- SIEM Monitoring
- Endpoint Monitoring
- Network Intrusion Detection
- IDS/IPS Operations
- Threat Detection
- Log Analysis
- Incident Investigation
- Malware Analysis
- Threat Intelligence
- Vulnerability Identification
- Security Event Correlation

---

# 🔍 Implemented Use Cases

## ✅ File Integrity Monitoring (FIM)
Monitored critical files and directories for unauthorized modifications and suspicious changes.

🔗 [File Integrity Monitoring Lab Report](https://github.com/ilolokerry/Endpoint-Monitoring-Threat-Detection-Lab-with-Wazuh/blob/main/03-Hands%20on%20lab%201-%20File%20Integrity%20Monitoring.md)


---

## ✅ Network Intrusion Detection & Prevention
Integrated Suricata as an IDS/IPS solution to detect:
- Port scanning
- Brute-force activity
- Web attack patterns
- Suspicious network traffic
- Potential command-and-control communication

🔗 Project Link:  

---

## ✅ SSH Brute-Force Detection
Detected repeated failed authentication attempts and suspicious login behavior.

🔗 Project Link:  


---

## ✅ Malicious Command Monitoring
Monitored suspicious command execution and PowerShell activity to identify potentially malicious behavior.

🔗 Project Link:  


---

## ✅ Vulnerability Detection
Performed vulnerability identification and monitoring across monitored systems.

🔗 Project Link:  

---

## ✅ Malware Analysis Workflows
Investigated suspicious files and analyzed indicators of compromise using malware analysis workflows and threat intelligence checks.

🔗 Project Link:  

---

# 🚨 Attack Scenarios Simulated

- SSH brute-force attacks
- Port scanning and reconnaissance
- Suspicious command execution
- Malicious file detection
- Web-based attack activity
- Unauthorized file modification attempts

---

# 📊 SOC Operations Performed

- Alert monitoring and triage
- Log analysis and investigation
- Threat detection and correlation
- IOC investigation
- Incident documentation
- Attack pattern analysis

---

# 📈 Skills Demonstrated

- Security Monitoring
- Threat Detection
- SIEM Operations
- IDS/IPS Monitoring
- Incident Response
- Threat Hunting
- Endpoint Security
- Network Security Analysis
- Log Correlation
- Security Investigation

---

# 🚀 Future Improvements

- Threat intelligence feed integration
- Automated alert response workflows
- Advanced detection rules
- Threat hunting dashboards
- Email security monitoring
- SOAR integration

---

# 🧠 Project Goal

This project was created to develop practical SOC analyst and blue team skills through hands-on security monitoring, attack detection, and incident investigation in a controlled lab environment.
