
# 🛡️ Hands-On Lab 4 – Detecting and Blocking SSH Brute-Force Attacks with Wazuh

---

# 📌 Overview

This hands-on lab demonstrates how Wazuh can detect and automatically respond to SSH brute-force attack activity using Active Response.

The objective of this lab was to:
- Identify the SSH brute-force detection rule
- Configure Active Response using `firewall-drop`
- Simulate repeated failed SSH authentication attempts
- Automatically block malicious source IP addresses
- Validate detection and response actions within the Wazuh dashboard

---

# 🎯 Lab Objective

The goal of this exercise was to simulate how a SOC analyst can:
- Detect SSH brute-force activity
- Investigate authentication attack alerts
- Configure automated defensive actions
- Block malicious IP addresses in real time

---

# 🔍 Step 1 – Identify the SSH Brute-Force Detection Rule

The Wazuh web interface was used to identify the SSH brute-force attack detection rule.

## Navigate to Rules

Within the Wazuh dashboard:
- Open **Rules**
- Search for Rule ID:

```text
5763
```

This rule is responsible for detecting SSH brute-force authentication activity.

The rule was selected because it would later be linked to the Active Response configuration.

📸 Screenshot Placeholder:
- Wazuh Rules page
- Rule 5763 search result
- Rule description and severity level

---

# ⚙️ Step 2 – Verify Firewall-Drop Active Response Command

The Wazuh manager configuration was reviewed to ensure the `firewall-drop` command was available for Active Response.

---

## Verify Active Response Binary Exists

Navigate to the Active Response directory:

```bash
cd /var/ossec/active-response/bin
```

Verify that `firewall-drop` exists within the directory.

📸 Screenshot Placeholder:
- Active response directory contents
- `firewall-drop` script visible

---

# 🛡️ Step 3 – Configure Active Response

The Active Response configuration was added to the Wazuh manager configuration file.

---

## Open Wazuh Configuration

```bash
sudo nano /var/ossec/etc/ossec.conf
```

---

## Add Active Response Configuration

```xml
<active-response>
  <command>firewall-drop</command>
  <location>local</location>
  <rules_id>5763</rules_id>
  <timeout>180</timeout>
</active-response>
```

---

# 🧠 Configuration Explanation

- `<command>firewall-drop</command>`  
  → Executes the firewall blocking action

- `<location>local</location>`  
  → Runs the response locally on the monitored system

- `<rules_id>5763</rules_id>`  
  → Triggers the response when Rule 5763 fires

- `<timeout>180</timeout>`  
  → Blocks the attacking IP for 180 seconds

📸 Screenshot Placeholder:
- Active Response configuration inside `ossec.conf`
- Highlighted Active Response section

---

# 🔄 Restart Wazuh Manager

After saving the configuration, the Wazuh manager service was restarted.

```bash
sudo systemctl restart wazuh-manager
```

---

## Verify Service Status

```bash
sudo systemctl status wazuh-manager
```

📸 Screenshot Placeholder:
- Wazuh manager restarted successfully
- Service running status

---

# ⚔️ Step 4 – SSH Brute-Force Simulation

A controlled SSH authentication failure simulation was performed within the lab environment to generate brute-force detection alerts.

---

# 🐧 Configure SSH on Ubuntu Endpoint

Install and enable SSH service on the monitored endpoint.

## Install OpenSSH Server

```bash
sudo apt install openssh-server -y
```

---

## Start SSH Service

```bash
sudo systemctl start ssh
```

---

## Enable SSH on Boot

```bash
sudo systemctl enable ssh
```

📸 Screenshot Placeholder:
- SSH service running
- SSH status confirmation

---

# 🛠️ Install Testing Tool on Attacker System

A password auditing tool was installed on the attacker machine within the isolated lab environment.

📸 Screenshot Placeholder:
- Tool installation output
- Attacker VM terminal

---

# 📄 Create Test Password List

A sample password list containing test entries was created for the simulation.

📸 Screenshot Placeholder:
- Password list file
- Example test entries

---

# 🔁 Simulate Repeated Authentication Failures

Repeated failed SSH authentication attempts were generated against the target endpoint in the isolated lab environment.

This activity triggered the Wazuh SSH brute-force detection rule.

📸 Screenshot Placeholder:
- Failed SSH login attempts
- Authentication failure logs

---

# 🚨 Step 5 – Confirm Detection and Blocking

The Wazuh dashboard was monitored to confirm:
- SSH brute-force detection alerts
- Rule 5763 activation
- Active Response execution
- Automatic firewall blocking

The blocked source IP was verified using firewall inspection commands.

---

## Verify Firewall Rules

```bash
sudo iptables -L -n --line-numbers
```

📸 Screenshot Placeholder:
- Wazuh brute-force alert
- Rule 5763 alert details
- Firewall block rule showing attacker IP
- Active Response logs

---

# 📊 Observations

The lab successfully demonstrated how Wazuh can:
- detect repeated failed SSH login attempts
- generate high-severity alerts
- automatically block malicious IP addresses
- improve endpoint protection through Active Response

---

# 🧠 Skills Practiced

- SSH monitoring
- Wazuh Active Response configuration
- Detection engineering
- Firewall rule verification
- Security alert investigation
- Brute-force attack detection
- SOC incident response workflows

---

# 🚀 Next Steps

- Configure email alerting for brute-force attacks
- Create dashboards for blocked IP activity
- Integrate GeoIP threat intelligence
- Add Suricata network-based SSH detection
- Correlate SSH attacks with endpoint telemetry
