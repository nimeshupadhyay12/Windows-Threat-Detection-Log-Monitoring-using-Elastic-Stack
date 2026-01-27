

# 🛡️ Windows Threat Detection & Log Monitoring using Elastic Stack

## 📌 Project Overview
This project demonstrates the implementation of a Windows-based threat detection and log monitoring system using the Elastic Stack. The primary objective is to collect, analyze, and detect suspicious activities—especially PowerShell-based attacks—from a Windows machine in near real time. Elastic Agent is deployed on the Windows host and centrally managed using Fleet Server. Logs are ingested into Elasticsearch and analyzed in Kibana, where custom detection rules are created to generate alerts. The project reflects real-world SOC detection engineering workflows and forms the foundation for a scalable threat intelligence platform.

---

## 🏗️ Architecture

### High-Level Architecture Diagram

```text
+-------------------+
|   Windows Host    |
|-------------------|
| PowerShell Logs   |
| Security Logs     |
| System Logs       |
+---------+---------+
          |
          | Elastic Agent
          v
+-------------------+
|   Fleet Server    |
|-------------------|
| Agent Management  |
| Policy Control   |
+---------+---------+
          |
          v
+-------------------+
|  Elasticsearch   |
|-------------------|
| Log Indexing     |
| Data Storage     |
+---------+---------+
          |
          v
+-------------------+
|     Kibana        |
|-------------------|
| Log Analysis     |
| Detection Rules  |
| Alerts           |
| Dashboards       |
+-------------------+

```

## 🔁 Attack → Detection → Dashboard Flow

### 1️⃣ Attack / Activity Simulation
- PowerShell commands are executed manually on the Windows machine
- Includes both normal and suspicious commands such as:
  - Encoded PowerShell commands
  - Script execution
  - Suspicious command-line arguments
- These actions simulate real-world attacker behavior, including:
  - Living-off-the-Land (LoLBins) techniques
  - Abuse of native Windows utilities for post-exploitation

---

### 2️⃣ Log Collection
- Elastic Agent is installed on the Windows host
- The agent is enrolled into Fleet Server using a managed agent policy
- Logs collected include:
  - `windows.powershell`
  - `windows.security`
  - `windows.system`
- The following telemetry is captured:
  - Process creation events
  - Command-line arguments
  - Execution metadata
- Logs are securely forwarded to Elasticsearch for indexing and analysis

---

### 3️⃣ Detection Engineering (Kibana Rules)
- Custom detection rules are created in Kibana using Kibana Query Language (KQL)
- Detection rules focus on identifying:
  - Encoded PowerShell execution
  - Suspicious PowerShell command patterns
  - Abnormal or unusual process behavior
- Rules are designed to reflect real-world attack techniques
- Detection logic can be extended to:
  - MITRE ATT&CK tactics and techniques
  - Advanced behavioral-based detections

---

### 4️⃣ Alerts & Dashboards
- When a detection rule is triggered:
  - Alerts are generated and displayed in the Kibana Security Alerts panel
- Dashboards are created to visualize:
  - PowerShell execution trends over time
  - Frequency of suspicious command execution
  - Detection rule hits and alert counts
- Dashboards provide:
  - SOC-style visibility
  - Centralized monitoring of host-based attacks
  - Quick investigation capabilities

---

## 🧰 Tech Stack

### Elastic Stack
- **Elasticsearch**
  - Log storage, indexing, and high-speed search
- **Kibana**
  - Log analysis
  - Detection rules
  - Alerting
  - Dashboards
- **Fleet Server**
  - Centralized Elastic Agent management
  - Policy enforcement
- **Elastic Agent**
  - Windows log collection
  - PowerShell and security telemetry ingestion

---

### Operating System
- **Windows**
  - Log source
  - Attack simulation environment

---

### Detection & Querying
- **Kibana Query Language (KQL)**
  - Used for log filtering
  - Detection rule logic
  - Threat hunting

---

### Security Domains
- Windows Event Monitoring
- Detection Engineering
- Log Analysis
- PowerShell Threat Detection
- SOC & Blue Team Operations

