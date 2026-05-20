
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

#  Step 1 – Identify the SSH Brute-Force Detection Rule

The Wazuh web interface was used to identify the SSH brute-force attack detection rule.

Navigate to Rules

Within the Wazuh dashboard:
- Open **Rules**
- Search for Rule ID:

```text
5763
```

This rule is responsible for detecting SSH brute-force authentication activity.

The rule was selected because it would later be linked to the Active Response configuration.

![rule](https://github.com/ilolokerry/Endpoint-Monitoring-Threat-Detection-Lab-with-Wazuh/blob/e17a2af450a953258c9cd715641041aa79233f24/images/bfa/local%20rules.png)
- Rule description and severity level

---

#  Step 2 – Verify Firewall-Drop Active Response Command

The Wazuh manager configuration was reviewed to ensure the `firewall-drop` command was available for Active Response.

---

Verify Active Response Binary Exists

Navigate to the Active Response directory:

```bash
cd /var/ossec/active-response/bin
```

Verify that `firewall-drop` exists within the directory.

![script](https://github.com/ilolokerry/Endpoint-Monitoring-Threat-Detection-Lab-with-Wazuh/blob/e17a2af450a953258c9cd715641041aa79233f24/images/bfa/fire%20wall%20rules.png)
- Active response directory contents
- `firewall-drop` script visible

---

#  Step 3 – Configure Active Response

The Active Response configuration was added to the Wazuh manager configuration file.

---

Open Wazuh Configuration

```bash
sudo nano /var/ossec/etc/ossec.conf
```

---

 Add Active Response Configuration

```xml
<active-response>
  <command>firewall-drop</command>
  <location>local</location>
  <rules_id>5763</rules_id>
  <timeout>180</timeout>
</active-response>
```
This configuration uses the `firewall-drop` active response to automatically block IP addresses for 180 seconds whenever Wazuh Rule `5763` detects an SSH brute-force attack on the monitored system.
---

 Restart Wazuh Manager

After saving the configuration, the Wazuh manager service was restarted.

```bash
sudo systemctl restart wazuh-manager
```

---

Verify Service Status

```bash
sudo systemctl status wazuh-manager
```

![response](https://github.com/ilolokerry/Endpoint-Monitoring-Threat-Detection-Lab-with-Wazuh/blob/e17a2af450a953258c9cd715641041aa79233f24/images/bfa/active.png)
---

#  Step 4 – SSH Brute-Force Simulation

A controlled SSH authentication failure simulation was performed within the lab environment to generate brute-force detection alerts.

---

 Configure SSH on Ubuntu Endpoint

Install and enable SSH service on the monitored endpoint.

```bash
sudo apt install openssh-server -y
sudo systemctl start ssh
sudo systemctl enable ssh
```
---

Install Hydra on attacker system

```bash
sudo apt update
sudo apt install hydra -y
```
---
Create a custom password list file (`PASSWD_LIST.txt`)  containing multiple test entries to simulate repeated authentication attempts against the target SSH service.

---
 Simulate SSH Brute-Force Attack

Repeated failed SSH authentication attempts were generated using Hydra against the target endpoint to simulate a brute-force attack scenario.

## Command used:

```bash
sudo hydra -t 4 -l <user> -P PASSWD_LIST.txt <victim_IP> ssh
```
![bfa](https://github.com/ilolokerry/Endpoint-Monitoring-Threat-Detection-Lab-with-Wazuh/blob/e17a2af450a953258c9cd715641041aa79233f24/images/bfa/bfa.png)
attack command

---

# Step 5 – Confirm Detection and Blocking

The Wazuh dashboard was monitored to confirm:
- SSH brute-force detection alerts
- Rule 5763 activation
- Active Response execution
- Automatic firewall blocking

![alerts](https://github.com/ilolokerry/Endpoint-Monitoring-Threat-Detection-Lab-with-Wazuh/blob/e17a2af450a953258c9cd715641041aa79233f24/images/bfa/alert.png)
![details]()
---
#  Observations

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
