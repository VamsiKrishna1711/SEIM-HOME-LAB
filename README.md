# SIEM Home Lab using Splunk, Sysmon & Kali Linux

## Project Overview

This project demonstrates the implementation of a Security Information and Event Management (SIEM) home lab designed to simulate a basic Security Operations Center (SOC) environment. The lab was built using Splunk Enterprise, Sysmon, Windows 10, Kali Linux, and VirtualBox to collect, monitor, and analyze security-related events generated within a controlled virtual environment.

The primary objective of the project was to gain hands-on experience with:

- Centralized log collection
- Windows event monitoring
- Endpoint telemetry analysis
- Security event investigation
- Threat detection workflows
- SIEM dashboard creation
- Alert generation and monitoring
- MITRE ATT&CK mapping

This project helped develop practical SOC analyst and cybersecurity monitoring skills through real-time security event analysis.

---

# Architecture

```text
+----------------+
| Kali Linux VM  |
| (Attacker VM)  |
+----------------+
          |
          v
+---------------------------+
| Windows 10 VM + Sysmon    |
| Endpoint Monitoring Agent |
+---------------------------+
          |
          v
+---------------------------+
| Splunk Enterprise SIEM    |
| Log Collection & Analysis |
+---------------------------+
          |
          v
+---------------------------+
| Dashboards, Alerts & SOC  |
| Monitoring Workflows      |
+---------------------------+
```

---

# Technologies and Tools Used

| Tool | Purpose |
|---|---|
| Splunk Enterprise | SIEM platform for centralized logging and analysis |
| Sysmon | Windows system monitoring and telemetry collection |
| Kali Linux | Security testing and attacker simulation VM |
| Windows 10 | Endpoint machine for log generation |
| VirtualBox | Virtualization platform for lab environment |
| Windows Event Logs | Native Windows logging source |

---

# Lab Components

## 1. Splunk Enterprise

Splunk Enterprise was configured as the central SIEM platform for collecting and analyzing logs generated from the Windows endpoint.

### Key Functions
- Centralized log aggregation
- Security event searching
- Dashboard visualization
- Alert generation
- Threat monitoring

### Access
```text
http://127.0.0.1:8000
```

---

## 2. Sysmon

Sysmon (System Monitor) from Microsoft Sysinternals was installed on the Windows 10 VM to generate detailed endpoint telemetry.

### Monitored Activities
- Process creation
- Network connections
- File modifications
- Command execution
- PowerShell activity

### Example Sysmon Event IDs

| Event ID | Description |
|---|---|
| 1 | Process Creation |
| 3 | Network Connection |
| 7 | Image Loaded |
| 11 | File Creation |

---

## 3. Windows 10 VM

The Windows 10 virtual machine acted as the monitored endpoint system.

### Activities Performed
- Command prompt execution
- Network browsing
- PowerShell commands
- Login attempt simulations

The generated telemetry was forwarded to Splunk using the Splunk Universal Forwarder.

---

## 4. Kali Linux VM

Kali Linux was used as the attacker simulation environment.

### Planned Activities
- Network reconnaissance
- Port scanning
- Enumeration
- Security testing

### Tools Available
- Nmap
- Burp Suite
- Hydra
- Wireshark

---

# Splunk Dashboards Implemented

## 1. Process Creation Events

Monitors process execution activity collected through Sysmon.

### Query
```spl
EventCode=1
```

### Purpose
- Detect suspicious processes
- Monitor command execution
- Identify abnormal activity

---

## 2. Network Connections

Monitors outbound and inbound network activity.

### Query
```spl
EventCode=3
```

### Purpose
- Monitor network communication
- Detect unusual connections
- Identify scanning behavior

---

## 3. Failed Login Attempts

Tracks failed Windows authentication attempts.

### Query
```spl
EventCode=4625
```

### Purpose
- Detect brute-force attempts
- Monitor authentication failures
- Investigate suspicious logins

---

## 4. Top Running Processes

Displays the most frequently executed processes.

### Query
```spl
EventCode=1 | stats count by Image
```

### Purpose
- Analyze process trends
- Identify frequently executed applications
- Detect unusual processes

---

# Splunk Alerts Configured

## Failed Login Detection Alert

### Query
```spl
EventCode=4625
```

### Trigger Condition
- More than 5 failed logins within 5 minutes

### MITRE Mapping
- T1110 – Brute Force

### Purpose
This alert simulates basic SOC monitoring functionality by automatically detecting suspicious authentication failures.

---

# Threat Hunting Queries

## Process Monitoring
```spl
EventCode=1
```

## Network Monitoring
```spl
EventCode=3
```

## Failed Logins
```spl
EventCode=4625
```

## Successful Logins
```spl
EventCode=4624
```

## Process Frequency Analysis
```spl
EventCode=1 | stats count by Image
```

---

# MITRE ATT&CK Mapping

| Detection | Splunk Query | MITRE Technique | Description |
|---|---|---|---|
| Process Creation | `EventCode=1` | T1059 | Command and Scripting Interpreter |
| Network Connections | `EventCode=3` | T1046 | Network Service Scanning |
| Failed Login Attempts | `EventCode=4625` | T1110 | Brute Force |
| Successful Logins | `EventCode=4624` | T1078 | Valid Accounts |
| PowerShell Activity | `powershell` | T1059.001 | PowerShell |

---

# Skills Demonstrated

## Cybersecurity Skills
- SIEM Deployment
- Security Monitoring
- Log Analysis
- Threat Detection
- Threat Hunting
- Endpoint Monitoring
- Windows Event Analysis
- Alert Configuration
- Security Operations Center (SOC) Concepts

## Technical Skills
- Splunk Enterprise
- Sysmon
- Windows Event Logs
- Kali Linux
- VirtualBox
- Windows Administration
- Basic Network Monitoring
- MITRE ATT&CK Framework

---

# Challenges Faced During Implementation

- Configuring Splunk Universal Forwarder
- Troubleshooting Sysmon log ingestion
- Configuring virtual machine networking
- Setting up dashboard visualizations
- Managing VM communication within VirtualBox

These challenges helped improve troubleshooting and system administration skills.

---

# Future Improvements

The following enhancements are planned for future versions of the project:

- Active Directory integration
- Wazuh deployment
- Sigma rule implementation
- Advanced threat hunting queries
- Brute-force attack simulations
- Automated alert notifications
- MITRE ATT&CK dashboard integration
- Vulnerability scanning integration

---

# Conclusion

This project provided hands-on experience with building and managing a SIEM-based cybersecurity monitoring environment. Through the implementation of Splunk, Sysmon, and Windows event monitoring, the lab successfully simulated foundational SOC workflows including log collection, event analysis, dashboard creation, and security alerting.

The project significantly improved practical understanding of:

- Security monitoring
- Endpoint telemetry
- SIEM operations
- Windows event logging
- Threat detection workflows
- Cybersecurity investigation techniques

---
