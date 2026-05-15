# 📊 Wazuh Dashboard Creation & Alert Visualization

---

## 📌 Project Overview

As part of my SOC Home Lab project using :contentReference[oaicite:0]{index=0}, I created custom dashboards to visualize and analyze security alerts inside the SIEM environment.

The objective of this phase was to improve alert visibility, monitor security events more efficiently, and gain hands-on experience building SOC-style dashboards for threat monitoring and analysis.

---

# 🎯 Goals

The dashboard was designed to:

- Monitor security alerts in real time
- Visualize the most common alerts
- Track total alert volume
- Display files detected by VirusTotal
- Improve SOC visibility and alert analysis workflows

---

# Step 1 – Import Sample Data into Wazuh

Before creating visualizations, sample security alert data was imported into the SIEM environment for analysis and dashboard testing.

📸 Screenshot Placeholder:
- Sample data successfully imported
- Wazuh Discover page showing alerts

---

# Step 2 – Create Top 10 Alerts Pie Chart

The first visualization created was a pie chart displaying the Top 10 security alerts detected within the last 24 hours.

## Configuration

### Visualization Type
- Pie Chart

### Data Source
- `alert.source`

### Metric Settings
- Aggregation: `Count`
- Custom Label: `Alerts`

### Bucket Settings
- Split Slices
- Aggregation: `Terms`
- Field: `rule.description`
- Order By: `Metric: Alerts`
- Order: `Descending`
- Size: `10`

This configuration grouped alerts by rule description and displayed the most frequent alerts as individual slices in the chart.

After configuration, the visualization was saved and added to the dashboard.

📸 Screenshot Placeholder:
- Pie chart configuration
- Final Top 10 Alerts pie chart
- Dashboard with pie chart added

---

# Step 3 – Create Total Alerts Metric

The second visualization created was a metric panel showing the total number of alerts generated in the environment.

## Configuration

### Visualization Type
- Metric

### Data Source
- `alert.source`

### Metric Settings
- Aggregation: `Count`
- Custom Label: `Total Alerts`

This metric provides quick visibility into the total alert volume detected by the SIEM.

📸 Screenshot Placeholder:
- Metric configuration
- Total alerts metric visualization

---

# Step 4 – Create VirusTotal Detection Table

The final visualization created was a table displaying files detected as malicious by VirusTotal integration.

This visualization helps identify potentially malicious files detected on monitored endpoints.

## Visualization Type
- Table

## Data Source
- `alert.source`

## Filter Applied

``` id="7rfj3h"
data.virustotal.found:1
```

This filter displays only alerts where VirusTotal identified a malicious file.

---

## Fields Added

The following fields were added to the table buckets section:

- `agent.ip`
- `data.virustotal.found`
- `data.virustotal.permalink`
- `data.virustotal.source.file`
- `data.virustotal.source.sha1`
- `timestamp`

Each field was limited to:
- Top 5 results
- Descending order

This configuration provided detailed visibility into detected malicious files, affected endpoints, associated hashes, and VirusTotal analysis links.

📸 Screenshot Placeholder:
- Table visualization configuration
- VirusTotal detection results
- Table added to dashboard

---

# Step 5 – Configure Dashboard Time Filter

A dashboard filter was added to display only alerts from the last 24 hours.

This helps ensure the dashboard focuses on recent security activity and improves SOC monitoring efficiency.

📸 Screenshot Placeholder:
- Time filter configuration
- Dashboard showing last 24 hours selected

---

# Step 6 – Save Dashboard

The completed dashboard was saved under the name:

``` id="4d2z2q"
Alerts
```

The dashboard now provides centralized visibility into:
- Alert trends
- Alert volume
- Malware detections
- VirusTotal analysis results

📸 Screenshot Placeholder:
- Final completed dashboard
- Full dashboard overview

---

# Final Dashboard Features

The completed dashboard includes:

- Top 10 Alerts Pie Chart
- Total Alerts Metric
- VirusTotal Detection Table
- 24-Hour Time Filter

---

#  Skills Practiced

Through this project, I gained hands-on experience with:

- SIEM dashboard creation
- Alert visualization
- Security data analysis
- Threat monitoring
- VirusTotal integration
- SOC workflow optimization
- Security event analysis

---


---

# 🎯 Project Goal

The purpose of this project is to build practical SOC analyst skills by creating real-world security monitoring dashboards for threat detection, visibility, and incident investigation.
