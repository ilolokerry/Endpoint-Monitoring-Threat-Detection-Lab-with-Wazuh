
# SOC Lab – Endpoint Monitoring & Threat Detection with Wazuh

##  Project Overview

This project is a hands-on SOC (Security Operations Center) lab designed to simulate real-world security monitoring and threat detection operations using endpoint and network telemetry.

The lab focuses on detecting, analyzing, and investigating malicious activity across endpoint and network environments through SIEM monitoring, IDS/IPS detection, log analysis, and threat investigation workflows.


---

# Objectives

- Build a practical SOC monitoring environment
- Detect malicious behavior and attack patterns
- Investigate security alerts and suspicious events
- Practice incident response and threat analysis workflows
- Simulate real-world blue team operations

---

#  Lab Architecture

```text
                 ┌──────────────────────┐
                 │   Attacker VM        │
                 │ (Kali / Test System) │
                 └──────────┬───────────┘
                            │
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

# Technologies & Concepts

- SIEM Monitoring
- Endpoint Monitoring
- Network analysis
- Threat Detection
- Log Analysis
- Incident Investigation
- Malware Analysis
- Threat Intelligence
- Vulnerability Identification
- Security Event Correlation

---

#  Implemented Use Cases

##  File Integrity Monitoring (FIM)
Monitored critical files and directories for unauthorized modifications and suspicious changes.

🔗 [File Integrity Monitoring Lab Report](https://github.com/ilolokerry/Endpoint-Monitoring-Threat-Detection-Lab-with-Wazuh/blob/main/03-Hands%20on%20lab%201-%20File%20Integrity%20Monitoring.md)


---

## SSH Brute-Force Detection
Detected repeated failed authentication attempts and suspicious login behavior.

🔗 [Detecting and Blocking SSH Brute-Force Attacks with Wazuh](https://github.com/ilolokerry/Endpoint-Monitoring-Threat-Detection-Lab-with-Wazuh/blob/60baa79113ba277db6b0279798b0d48755d1de15/06-Hands-on-lab%204-Detecting%20and%20Blocking%20SSH%20Brute%20force%20attackes.md)


---

## Malicious Command Monitoring
Monitored suspicious command execution and PowerShell activity to identify potentially malicious behavior.

🔗 [Detecting Malicious Commands with wazuh](https://github.com/ilolokerry/Endpoint-Monitoring-Threat-Detection-Lab-with-Wazuh/blob/71ebf4210dd76243cd9129b2cb7cdf83fdbca561/05-Hands-On%20Lab%203%20%E2%80%93%20Detecting%20The%20Execution%20of%20Malicious%20Commands.md)


---

##  Vulnerability Detection
Performed vulnerability identification and monitoring across monitored systems.

🔗 [Vulnerability Detection with Wazuh](https://github.com/ilolokerry/Endpoint-Monitoring-Threat-Detection-Lab-with-Wazuh/blob/71ebf4210dd76243cd9129b2cb7cdf83fdbca561/04-Hands%20on%20lab%202-Vulnrebilty%20Detection.md)

---

##  Detecting Malicious Files with Wazuh & VirusTotal
Investigated suspicious files using VirusTotal integration within Wazuh to identify malicious file activity, analyze threat intelligence results, and validate malware detection alerts.

🔗 [Detecting Malicious Files with Wazuh & VirusTotal](https://github.com/ilolokerry/Endpoint-Monitoring-Threat-Detection-Lab-with-Wazuh/blob/71ebf4210dd76243cd9129b2cb7cdf83fdbca561/07-Hands-on-lab%205-Detecting%20Malicous%20files%20with%20Virustotal.md)

---

#  SOC Operations Performed

- Alert monitoring and triage
- Log analysis and investigation
- Threat detection and correlation
- IOC investigation
- Incident documentation
- Attack pattern analysis

---

# Skills Demonstrated

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

#  Future Improvements

- Threat intelligence feed integration
- Automated alert response workflows
- Advanced detection rules
- Threat hunting dashboards
- Email security monitoring
- SOAR integration

---

