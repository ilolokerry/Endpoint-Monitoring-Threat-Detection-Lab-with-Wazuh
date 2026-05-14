
# 🛡️ SOC Home Lab Setup – Wazuh SIEM Environment 

---

## 📌 What is Wazuh?

Wazuh is an open-source security monitoring and threat detection platform used for endpoint security, log analysis, intrusion detection, and incident response.

It functions as a Security Information and Event Management (SIEM) solution that collects and analyzes security telemetry from multiple systems in real time.

---

## ⚙️ Key Capabilities of Wazuh

Wazuh provides the following security capabilities:

- 📊 Centralized log collection and analysis
- 🖥️ Endpoint monitoring
- 🔍 File Integrity Monitoring (FIM)
- 🚨 Intrusion detection and alerting
- 🌐 Security event correlation (SIEM functionality)
- 🧠 Threat intelligence integration
- 🛡️ Vulnerability detection and assessment
- 📡 Active response and automation

---

## 🎯 Why This Lab Was Built

This lab was created to simulate a real-world SOC environment where security analysts:

- Monitor endpoints in real time
- Detect malicious activity and anomalies
- Investigate security alerts
- Perform incident response
- Correlate network and endpoint events

Goal: build practical SOC analyst skills using real infrastructure and attack simulations.

---

# 🌐 Step 0 – Network & DHCP Configuration

Before setting up the lab machines, the network was configured for proper IP allocation.

## DHCP Configuration

The DHCP server was configured to assign IP addresses starting from:

```
10.0.0.10
```

This ensures:
- Controlled IP range for all lab devices
- Easier endpoint tracking
- Better SOC visibility during investigations

📸 Screenshot Placeholder:
- DHCP range configuration (10.0.0.10 start IP)
- Virtual network settings

---

# 🧱 Lab Architecture

The environment consists of:

- 🐉 Kali Linux (Attacker VM)
- 💀 Metasploitable 2 (Vulnerable Target)
- 🐧 Ubuntu Desktop 2026 (Client)
- 🪟 Windows 10 Pro (Endpoint)
- 🖥️ Ubuntu Server 2026 (Wazuh SIEM Server)

---

# ⚙️ Step 1 – Install Kali Linux

Kali Linux is used for attack simulation and penetration testing.

```bash
sudo apt update && sudo apt upgrade -y
```

📸 Screenshot Placeholder:
- Kali setup complete
- System update output

---

# 💀 Step 2 – Install Metasploitable 2

Used as a vulnerable target for attack simulation.

📸 Screenshot Placeholder:
- VM login screen
- IP address output

---

# 🐧 Step 3 – Install Ubuntu Desktop (Client)

Used to access dashboards and monitor alerts.

```bash
sudo apt update && sudo apt upgrade -y
```

📸 Screenshot Placeholder:
- Ubuntu desktop
- Network configuration

---

# 🪟 Step 4 – Install Windows 10 Pro

Used as a monitored endpoint.

📸 Screenshot Placeholder:
- Windows desktop
- Network settings

---

# 🖥️ Step 5 – Install Wazuh Server

```bash
curl -sO https://packages.wazuh.com/4.7/wazuh-install.sh
sudo bash wazuh-install.sh -a
```

This installs:
- Manager
- Indexer
- Dashboard

Verify:

```bash
sudo systemctl status wazuh-manager
```

📸 Screenshot Placeholder:
- Installation complete
- Service running

---

# 🌐 Step 6 – Access Wazuh Dashboard

```
https://<WAZUH-SERVER-IP>
```

Login:
- admin / generated password

📸 Screenshot Placeholder:
- Login page
- Dashboard view

---

# 🐧 Step 7 – Ubuntu Agent Enrollment

```bash
sudo apt install wazuh-agent -y
```

Configure:

```bash
sudo nano /var/ossec/etc/ossec.conf
```

```xml
<server>
  <address>WAZUH_SERVER_IP</address>
</server>
```

Start:

```bash
sudo systemctl enable wazuh-agent
sudo systemctl start wazuh-agent
```

📸 Screenshot Placeholder:
- Agent active in dashboard

---

# 🪟 Step 8 – Windows Agent Enrollment

Install Windows agent → configure:

```
C:\Program Files (x86)\ossec-agent\ossec.conf
```

```xml
<server>
  <address>WAZUH_SERVER_IP</address>
</server>
```

Start service:

```powershell
net start wazuh
```

📸 Screenshot Placeholder:
- Windows agent active
- Dashboard showing endpoint

---

# 📊 Final Summary

This SOC lab simulates:

- Endpoint monitoring
- Centralized SIEM logging
- Threat detection
- Attack simulation environment

---

# 🚀 Next Steps

- Add Suricata IDS/IPS
- Add Sysmon logging
- Create detection rules
- Run attack simulations
- Build SOC playbooks

---

# 🧠 Goal

Develop real SOC skills in:
- log analysis
- endpoint monitoring
- threat detection
- incident response
- SIEM operations
