
# 🛡️ Hands-On Lab 3 – Detecting Malicious Commands with Wazuh & Auditd

---

# 📌 Overview

This hands-on lab demonstrates how to detect suspicious and potentially malicious command execution on Linux endpoints using Wazuh and Auditd.

The lab focused on:
- Monitoring command execution activity
- Forwarding Auditd logs to Wazuh
- Creating custom detection rules
- Detecting suspicious tools such as Netcat
- Generating high-severity alerts for malicious command execution

---

# 🧠 What is Auditd?

Auditd (Audit Daemon) is part of the Linux auditing framework used for monitoring and logging system activity.

It helps system administrators and SOC analysts:
- Track command execution
- Monitor file access
- Record authentication activity
- Investigate security incidents
- Perform forensic analysis

---

# ⚙️ Key Functions of Auditd

- 📊 Event logging
- 🛡️ Rule enforcement
- 🚨 Alert generation
- 🔍 Forensic investigation
- 📁 File and process monitoring

---

# 🎯 Lab Objective

The objective of this lab was to:
- Monitor Linux command execution activity
- Detect suspicious programs using Wazuh
- Generate high-severity alerts for malicious commands
- Simulate attacker activity using Netcat

---

# ⚙️ Step 1 – Install and Enable Auditd on the Endpoint

Auditd was installed on the monitored Linux endpoint.

## Install Auditd

```bash
sudo apt -y install auditd
```

---

## Start Auditd Service

```bash
sudo systemctl start auditd
```

---

## Enable Auditd on Boot

```bash
sudo systemctl enable auditd
```

📸 Screenshot Placeholder:
- Auditd installation output
- Auditd service status

---

# 📂 Step 2 – Add Auditd Logs to the Wazuh Agent

The Auditd log file was added to the Wazuh agent configuration for monitoring.

---

## View Audit Logs in Real Time

```bash
sudo tail -f /var/log/audit/audit.log
```

This was used to verify that Auditd events were being generated successfully.

📸 Screenshot Placeholder:
- Real-time Auditd log generation
- Terminal showing audit events

---

## Open Wazuh Agent Configuration

```bash
sudo nano /var/ossec/etc/ossec.conf
```

---

## Add Audit Log Monitoring Configuration

```xml
<localfile>
  <log_format>audit</log_format>
  <location>/var/log/audit/audit.log</location>
</localfile>
```

---

## Restart Wazuh Agent

```bash
sudo systemctl restart wazuh-agent
```

📸 Screenshot Placeholder:
- Wazuh agent configuration
- Agent restart confirmation

---

# 🛡️ Step 3 – Add Auditd Rules

Auditd rules were configured to monitor command execution activity.

---

## Open Audit Rules File

```bash
sudo nano /etc/audit/audit.rules
```

---

## Add Command Execution Monitoring Rules

```bash
-a always,exit -F arch=b32 -S execve -k audit-wazuh-c
-a always,exit -F arch=b64 -S execve -k audit-wazuh-c
```

### Rule Explanation

- `execve` → Monitors executed commands
- `always,exit` → Logs every execution event
- `arch=b32 / b64` → Monitors both 32-bit and 64-bit commands
- `audit-wazuh-c` → Custom key used for tracking events

---

## Restart Auditd

```bash
sudo systemctl restart auditd
```

📸 Screenshot Placeholder:
- Audit rules added successfully
- Auditd restart confirmation

---

# 🚨 Step 4 – Configure Wazuh Detection Rules

A custom CDB list and custom Wazuh rule were created to detect suspicious command execution.

---

# 📂 Create Suspicious Program List

Create the file:

```bash
sudo nano /var/ossec/etc/lists/suspicious-programs
```

---

## Add Suspicious Programs

```text
ncat:yellow
nc:red
tcpdump:orange
```

### Severity Meaning

- `red` → Highly suspicious
- `orange` → Suspicious
- `yellow` → Monitoring recommended

📸 Screenshot Placeholder:
- Suspicious program list file
- Configured program entries

---

# ⚙️ Add List to Wazuh Configuration

Open the Wazuh manager configuration:

```bash
sudo nano /var/ossec/etc/ossec.conf
```

---

## Add the List Under `<ruleset>`

```xml
<list>etc/lists/suspicious-programs</list>
```

📸 Screenshot Placeholder:
- Wazuh configuration showing custom list

---

# 🛡️ Create Custom Detection Rule

Open local rules file:

```bash
sudo nano /var/ossec/etc/rules/local_rules.xml
```

---

## Add High-Severity Detection Rule

```xml
<group name="audit">
  <rule id="100210" level="12">
    <if_sid>80792</if_sid>

    <list field="audit.command"
          lookup="match_key_value"
          check_value="red">
          etc/lists/suspicious-programs
    </list>

    <description>
      Audit: Highly Suspicious Command Executed: $(audit.exe)
    </description>

    <group>audit_command,</group>
  </rule>
</group>
```

### Rule Purpose

This rule generates a high-severity alert whenever a command categorized as `red` is executed.

📸 Screenshot Placeholder:
- Custom Wazuh rule configuration
- Local rules XML file

---

# 🔄 Restart Wazuh Manager

```bash
sudo systemctl restart wazuh-manager
```

📸 Screenshot Placeholder:
- Wazuh manager restart output

---

# ⚔️ Step 5 – Attack Simulation with Netcat

Netcat was used to simulate suspicious command execution activity.

---

## Install Netcat on Endpoint

```bash
sudo apt -y install netcat
```

---

## Execute Netcat Command

```bash
nc -v
```

This activity triggered the custom Wazuh detection rule.

📸 Screenshot Placeholder:
- Netcat installation
- Netcat execution in terminal

---

# 🚨 Alert Detection

Wazuh successfully detected the execution of Netcat and generated a high-severity alert.

The alert included:
- Executed command
- Endpoint hostname
- Rule ID
- Severity level
- Timestamp
- Audit event details

📸 Screenshot Placeholder:
- Wazuh alert triggered by Netcat
- Rule ID 100210 alert details
- Alert severity visualization

---

# 📊 Observations

This lab demonstrated how Wazuh and Auditd can work together to:
- monitor Linux command execution
- detect suspicious tools
- generate real-time alerts
- improve endpoint visibility

The custom detection logic successfully identified Netcat execution as suspicious activity.

---

# 🧠 Skills Practiced

- Linux auditing
- Wazuh rule creation
- Detection engineering
- Endpoint monitoring
- Command execution monitoring
- Security alert investigation
- Threat detection workflows

---

# 🚀 Next Steps

- Detect reverse shell activity
- Add Active Response for malicious commands
- Monitor additional tools such as Nmap and Socat
- Integrate MITRE ATT&CK mappings
- Create command execution dashboards in Wazuh
