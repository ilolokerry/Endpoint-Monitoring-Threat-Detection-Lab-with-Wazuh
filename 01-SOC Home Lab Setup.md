
# 🛡️ SOC Home Lab Setup – Wazuh SIEM Environment 

---

## 📌 What is Wazuh?

Wazuh is an open-source security monitoring and threat detection platform used for endpoint security, log analysis, intrusion detection, and incident response.

It functions as a Security Information and Event Management (SIEM) solution that collects and analyzes security telemetry from multiple systems in real time.

---

## ⚙️ Key Capabilities of Wazuh

Wazuh provides the following security capabilities:

-  Centralized log collection and analysis
-  Endpoint monitoring
-  File Integrity Monitoring (FIM)
-  Intrusion detection and alerting
-  Security event correlation (SIEM functionality)
-  Threat intelligence integration
-  Vulnerability detection and assessment
-  Active response and automation

---

##  Why This Lab Was Built

This lab was created to simulate a real-world SOC environment where security analysts:

- Monitor endpoints in real time
- Detect malicious activity and anomalies
- Investigate security alerts
- Perform incident response
- Correlate network and endpoint events

Goal: build practical SOC analyst skills using real infrastructure and attack simulations.

---

# 🧱 Lab Architecture
All systems are virtual machines deployed inside VMware Workstation.
---

The environment consists of:

-  Kali Linux (Attacker VM)
-  Metasploitable 2 (Vulnerable Target)
-  Ubuntu Desktop 26 (Client)
-  Windows 10 Pro (Endpoint)
-  Ubuntu Server 26 (Wazuh Server)


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

![Virtual network settings](https://github.com/ilolokerry/Endpoint-Monitoring-Threat-Detection-Lab-with-Wazuh/blob/1c126bd119911b2d4d84844c6fdea27e62eb4728/images/wazuh/network%20settings.png)

-Virtual network settings
- DHCP range configuration (10.0.0.10 start IP)
  
---

# ⚙️ Step 1 – Install Kali Linux

Kali Linux is used for attack simulation and penetration testing.

## Download Source:
https://www.kali.org/get-kali/

to update the operating system via the command line
```
sudo apt update && sudo apt upgrade -y
```

![kali](https://github.com/ilolokerry/Endpoint-Monitoring-Threat-Detection-Lab-with-Wazuh/blob/1c126bd119911b2d4d84844c6fdea27e62eb4728/images/wazuh/kali%20vm.png)
- Kali setup complete

---

# 💀 Step 2 – Install Metasploitable 2

Used as a vulnerable target for attack simulation.

## Download Source:
https://sourceforge.net/projects/metasploitable/

![meta](https://github.com/ilolokerry/Endpoint-Monitoring-Threat-Detection-Lab-with-Wazuh/blob/1c126bd119911b2d4d84844c6fdea27e62eb4728/images/wazuh/meta%20vm.png)

- VM login screen

---

# 🐧 Step 3 – Install Ubuntu Desktop (Client)

Used to access dashboards and monitor alerts.

## Download Source:
https://ubuntu.com/download/desktop


to update the operating system via the command line
```
sudo apt update && sudo apt upgrade -y
```
![ubuntu](https://github.com/ilolokerry/Endpoint-Monitoring-Threat-Detection-Lab-with-Wazuh/blob/1c126bd119911b2d4d84844c6fdea27e62eb4728/images/wazuh/ubuntu%20vm.png)

- Ubuntu desktop
- Network configuration

---

# 🪟 Step 4 – Install Windows 10 Pro

Used as a monitored endpoint.

##  Download Source:
https://www.microsoft.com/software-download/windows10

![windows](https://github.com/ilolokerry/Endpoint-Monitoring-Threat-Detection-Lab-with-Wazuh/blob/1c126bd119911b2d4d84844c6fdea27e62eb4728/images/wazuh/windows%20vm.png)
- Windows desktop
- Network settings

---

# 🖥️ Step 5 – Install Wazuh Server

## Download Source:
https://ubuntu.com/download/server

to update the operating system via the command line
```
sudo apt update && sudo apt upgrade -y
```

```To begin wazuh installation
curl -sO https://packages.wazuh.com/4.7/wazuh-install.sh
sudo bash wazuh-install.sh -a
```
![wazuh innstallation](https://github.com/ilolokerry/Endpoint-Monitoring-Threat-Detection-Lab-with-Wazuh/blob/1c126bd119911b2d4d84844c6fdea27e62eb4728/images/wazuh/wazuh%20installation.png)
![wazuh installed](https://github.com/ilolokerry/Endpoint-Monitoring-Threat-Detection-Lab-with-Wazuh/blob/1c126bd119911b2d4d84844c6fdea27e62eb4728/images/wazuh/wazuh%20installation%20done.png)
This installs:
- Manager
- Indexer
- Dashboard

Verify:

```
sudo systemctl status wazuh-manager
```
![system check](https://github.com/ilolokerry/Endpoint-Monitoring-Threat-Detection-Lab-with-Wazuh/blob/1c126bd119911b2d4d84844c6fdea27e62eb4728/images/wazuh/wazuh%20server%20check.png)

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
  ![wazuh dashboard](https://github.com/ilolokerry/Endpoint-Monitoring-Threat-Detection-Lab-with-Wazuh/blob/1c126bd119911b2d4d84844c6fdea27e62eb4728/images/wazuh/wazuh%20dashboard.png)

- Dashboard view

---

# 🐧 Step 7 – Ubuntu Agent Enrollment

## Install agent
![agentdeploymenttab](https://github.com/ilolokerry/Endpoint-Monitoring-Threat-Detection-Lab-with-Wazuh/blob/1c126bd119911b2d4d84844c6fdea27e62eb4728/images/wazuh/agent%20deployment%20tab.png)
```bash
curl -s https://packages.wazuh.com/key/GPG-KEY-WAZUH | sudo gpg --dearmor -o /usr/share/keyrings/wazuh.gpg
echo "deb [signed-by=/usr/share/keyrings/wazuh.gpg] https://packages.wazuh.com/4.x/apt stable main" | sudo tee /etc/apt/sources.list.d/wazuh.list
sudo apt update
sudo apt install wazuh-agent -y
```
![agent install](https://github.com/ilolokerry/Endpoint-Monitoring-Threat-Detection-Lab-with-Wazuh/blob/1c126bd119911b2d4d84844c6fdea27e62eb4728/images/wazuh/ubuntu%20agent%20deployment.png)
Start:

```bash
systemctl daemon-reload
sudo systemctl enable wazuh-agent
sudo systemctl start wazuh-agent
```

![ubuntu agent active](https://github.com/ilolokerry/Endpoint-Monitoring-Threat-Detection-Lab-with-Wazuh/blob/1c126bd119911b2d4d84844c6fdea27e62eb4728/images/wazuh/ubuntu%20agent%20active.png)
- Agent active in dashboard

---

# 🪟 Step 8 – Windows Agent Enrollment

## Install agent (PowerShell as Admin)

```powershell
Invoke-WebRequest -Uri https://packages.wazuh.com/4.x/windows/wazuh-agent-4.7.0-1.msi -OutFile wazuh-agent.msi
msiexec.exe /i wazuh-agent.msi /q
```

Start service:

```powershell
net start wazuh
```
![both agents active](https://github.com/ilolokerry/Endpoint-Monitoring-Threat-Detection-Lab-with-Wazuh/blob/1c126bd119911b2d4d84844c6fdea27e62eb4728/images/wazuh/both%20agents%20active.png)
- Dashboard showing endpoint
-Both agents active

---

# 📊 Final Summary

This SOC lab simulates:

- Endpoint monitoring
- Centralized SIEM logging
- Threat detection
- Attack simulation environment

---

#  Next Steps

- Add Suricata IDS/IPS
- Add Sysmon logging
- Create detection rules
- Run attack simulations
- Build SOC playbooks

---

# Goals

Develop real SOC skills in:
- log analysis
- endpoint monitoring
- threat detection
- incident response
- SIEM operations
