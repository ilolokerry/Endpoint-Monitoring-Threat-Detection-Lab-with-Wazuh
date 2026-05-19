
# 🛡️ Hands-On Lab 3 – Vulnerability Detection with Wazuh

---

## 📌 Overview

This hands-on lab demonstrates how Wazuh can be used for vulnerability detection and management across monitored endpoints.

The objective of this lab was to:
- Enable vulnerability detection
- Configure vulnerability feeds
- Detect CVEs affecting monitored systems
- Visualize vulnerabilities within the Wazuh dashboard
- Review remediation recommendations

---

# ⚙️ Step 1 – Verify Vulnerability Detection Configuration

The Wazuh configuration file was opened to verify that vulnerability detection was enabled.

## Open Configuration File

```bash
sudo nano /var/ossec/etc/ossec.conf
```

---

## Vulnerability Detection Configuration

The following settings were verified:

```xml
<vulnerability-detection>
  <enabled>yes</enabled>
  <index-status>yes</index-status>
  <feed-update-interval>60m</feed-update-interval>
</vulnerability-detection>
```

📸 Screenshot Placeholder:
- Wazuh `ossec.conf` vulnerability detection configuration
- Terminal showing the configuration file

---

# 🔄 Step 2 – Restart Wazuh Manager

After verifying the configuration, the Wazuh manager service was restarted.

```bash
sudo systemctl restart wazuh-manager
```

---

## Verify Service Status

```bash
sudo systemctl status wazuh-manager
```

📸 Screenshot Placeholder:
- Wazuh manager successfully restarted
- Service status output

---

# 📊 Step 3 – Visualize Vulnerabilities in the Wazuh Dashboard

The Wazuh dashboard was used to visualize vulnerabilities detected on monitored agents.

The dashboard displayed:
- Vulnerable agent systems
- Related CVE identifiers
- Vulnerability severity levels
- CVE documentation and references
- Recommended remediation guidance

The vulnerability reports could also be exported for documentation and further analysis.

📸 Screenshot Placeholder:
- Vulnerability Detection dashboard overview
- Detected CVEs on monitored agents
- CVE details and remediation recommendations
- Export vulnerability report option

---

# 🔍 Observations

The vulnerability detection module successfully identified vulnerable software packages installed on monitored systems and mapped them to publicly known CVEs.

This demonstrated how Wazuh can provide:
- centralized vulnerability visibility
- real-time vulnerability monitoring
- remediation guidance for affected systems

---

# 📌 Key Features Demonstrated

- Vulnerability detection
- CVE identification
- Agent vulnerability visibility
- Security posture assessment
- Vulnerability feed integration
- Vulnerability report exporting

---

# 🧠 Skills Practiced

- Wazuh administration
- SIEM configuration
- Vulnerability management
- CVE analysis
- Security monitoring
- SOC investigation workflows

---

# 🚀 Next Steps

- Configure email alerting for critical CVEs
- Integrate threat intelligence feeds
- Perform vulnerability remediation testing
- Build custom vulnerability dashboards
- Correlate vulnerabilities with active threats
