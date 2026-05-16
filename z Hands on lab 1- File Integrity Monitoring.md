
# 🔍 File Integrity Monitoring (FIM) Lab with Wazuh

---

## 📌 Project Overview

As part of my SOC Home Lab project using :contentReference[oaicite:0]{index=0}, I performed a hands-on File Integrity Monitoring (FIM) lab to detect file system changes on a monitored Linux endpoint.

The objective of this lab was to configure real-time file monitoring, generate file modification events, and validate alert generation within the SIEM environment.

---

# 🎯 Lab Objectives

This lab was designed to:

- Enable File Integrity Monitoring (FIM)
- Monitor sensitive directories for changes
- Generate file creation activity
- Detect unauthorized file additions
- Validate alert generation in Wazuh
- Gain hands-on SOC monitoring experience

---

# 🖥️ Step 1 – Configure Wazuh Manager Logging

The first step was enabling detailed logging on the Wazuh server.

## Navigate to the Wazuh configuration file

```bash id="ayr4j4"
sudo nano /var/ossec/etc/ossec.conf
```

Under the `<global>` section, the following settings were enabled:

```xml id="fzd9t9"
<logall>yes</logall>

<logall_json>yes</logall_json>
```

These settings enable:
- Full alert logging
- JSON-formatted event logging
- Improved visibility for investigations and alert analysis

📸 Screenshot Placeholder:
- Wazuh server configuration file
- `<logall>` and `<logall_json>` enabled

---

# 🐧 Step 2 – Enable File Integrity Monitoring on Ubuntu Agent

The next step was enabling FIM on the Ubuntu client endpoint.

## Open the agent configuration file

```bash id="bck4a6"
sudo nano /var/ossec/etc/ossec.conf
```

Navigate to the File Integrity Monitoring section.

Under:

```xml id="vjlwm3"
<scan_on_start>yes</scan_on_start>
```

The following directory monitoring rule was added:

```xml id="6r3k3k"
<directories check_all="yes" report_changes="yes" realtime="yes">/root</directories>
```

This configuration enables:
- Real-time monitoring
- File change detection
- File addition monitoring
- Detailed reporting for the `/root` directory

📸 Screenshot Placeholder:
- FIM configuration section
- `/root` directory monitoring rule added

---

# 🔄 Step 3 – Restart Wazuh Agent

After modifying the configuration, the Wazuh agent was restarted to apply the changes.

```bash id="9b3s6k"
sudo systemctl restart wazuh-agent
```

Verify the agent status:

```bash id="vc4q8j"
sudo systemctl status wazuh-agent
```

📸 Screenshot Placeholder:
- Wazuh agent restarted successfully
- Service status output

---

# 📂 Step 4 – Generate File Creation Activity

To test File Integrity Monitoring, a new file was created inside the monitored `/root` directory.

## Create sample file

```bash id="ys78yk"
touch samplefile.txt
```

This action simulates:
- unauthorized file creation
- suspicious endpoint activity
- file system changes requiring SOC visibility

📸 Screenshot Placeholder:
- Terminal showing file creation
- `/root` directory contents

---

# 🚨 Step 5 – Confirm Alert Generation

After creating the file, the Wazuh dashboard was monitored for generated alerts.

The SIEM successfully detected the file creation event.

## Alert Details

- Rule Name: `File added to the system`
- Rule ID: `554`

This confirmed that:
- File Integrity Monitoring was functioning correctly
- Real-time monitoring was active
- Wazuh successfully detected file system changes

📸 Screenshot Placeholder:
- Wazuh alert showing file creation event
- Alert details panel
- Rule ID 554 information

---

# 📊 Investigation Summary

The generated alert provided visibility into:
- affected endpoint
- monitored directory
- file creation event
- detection timestamp
- triggered detection rule

This demonstrates how FIM can help SOC analysts detect:
- unauthorized file changes
- malware drops
- persistence mechanisms
- suspicious endpoint activity

---

# 🧠 Skills Practiced

Through this lab, I gained hands-on experience with:

- File Integrity Monitoring (FIM)
- Wazuh agent configuration
- Linux endpoint monitoring
- SIEM alert analysis
- Real-time security monitoring
- Threat detection workflows
- SOC investigation processes

---

# 🚀 Next Steps

Planned improvements include:

- Monitoring additional sensitive directories
- Detecting file modifications and deletions
- Integrating Sysmon telemetry
- Creating custom FIM detection rules
- Simulating malware file drops
- Building alert correlation dashboards

---

# 🎯 Goal of This Lab

The purpose of this lab is to build practical SOC analyst skills by detecting and investigating unauthorized file system activity using real-time endpoint monitoring and SIEM alerting.
