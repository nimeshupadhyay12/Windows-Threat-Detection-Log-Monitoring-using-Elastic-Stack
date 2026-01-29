# ⚙️ Project Setup & Implementation Guide

This document explains the complete setup and working of the **Windows Threat Detection & Log Monitoring using Elastic Stack** project.  
It covers the environment setup, log collection pipeline, attack simulation, detection rule creation, and alert validation.

---

## 📌 Project Objective

The objective of this project is to build a **host-based detection system** using the Elastic Stack to monitor Windows activity and detect malicious PowerShell behavior. The project simulates real-world attacker techniques and validates them using custom Kibana detection rules, similar to how a SOC operates.

---

## 🖥️ Environment Overview

### System Requirements
- Windows OS (used as victim + log source)
- Elasticsearch
- Kibana
- Fleet Server
- Elastic Agent
- Internet connectivity

### Role of Each Component
- **Windows**: Attack surface and telemetry source  
- **Elastic Agent**: Collects Windows logs  
- **Fleet Server**: Central agent and policy management  
- **Elasticsearch**: Stores and indexes logs  
- **Kibana**: Detection rules, alerts, dashboards (SIEM)

---

## 🏗️ Step 1: Install Elasticsearch & Kibana

1. Download Elasticsearch and Kibana from Elastic official website
2. Start Elasticsearch service
3. Start Kibana service
4. Verify access:
   - Elasticsearch → `http://localhost:9200`
   - Kibana → `http://localhost:5601`

Kibana is used as the central interface for log analysis and detection engineering.

---

## 🔗 Step 2: Configure Fleet Server

1. Open Kibana
2. Navigate to **Management → Fleet**
3. Enable Fleet
4. Install Fleet Server
5. Confirm Fleet Server status as **Healthy**

Fleet Server is responsible for managing Elastic Agents and policies.

---

## 🧲 Step 3: Install Elastic Agent on Windows

1. From Fleet → Agents → Add Agent
2. Select Windows platform
3. Copy the enrollment command
4. Run the command in Windows PowerShell (Administrator)

Once installed:
- The agent enrolls with Fleet Server
- Windows logs begin flowing into Elasticsearch

---

## 📥 Step 4: Enable Windows Log Collection

In Fleet Agent Policy:
- Add **Windows integration**
- Enable:
  - PowerShell logs
  - Security logs
  - System logs

Verify logs in Kibana Discover using:
- `data_stream.dataset : "windows.powershell"`
- `data_stream.dataset : "windows.security"`

---

## ⚔️ Step 5: Attack Simulation (PowerShell)

The following attacker-like behaviors were simulated on the Windows host:
- Base64 encoded PowerShell execution
- Execution policy bypass
- Hidden PowerShell execution
- Command Prompt spawning PowerShell
- Reconnaissance using `whoami` and `Get-Process`
- File download using `certutil`

These commands generated realistic telemetry used for detection testing.

---

## 🧠 Step 6: Detection Rule Creation (Kibana)

Custom detection rules were created in:
**Kibana → Security → Detection Rules**

### Rules Implemented
1. PowerShell Hidden Window Execution
2. Command Prompt Spawning PowerShell
3. PowerShell ExecutionPolicy Bypass
4. PowerShell Encoded Command Execution

Rules were written using **Kibana Query Language (KQL)** and mapped to suspicious PowerShell behaviors.

---

## 🚨 Step 7: Alert Validation

1. Re-run PowerShell attack commands
2. Navigate to **Security → Alerts**
3. Confirm alerts are generated for:
   - Encoded execution
   - Policy bypass
   - Hidden execution
   - Parent-child process abuse

Each alert includes:
- Host name
- User
- Command line
- Rule name
- Severity

---

## 📊 Step 8: Visualization & Monitoring

Dashboards were created to visualize:
- PowerShell execution activity
- Detection rule hits
- Suspicious command trends

These dashboards provide **SOC-style visibility** into host behavior.

---

## 🔍 How the Project Works (End-to-End)

1. Attacker executes PowerShell commands on Windows
2. Windows generates event logs
3. Elastic Agent collects logs
4. Fleet Server manages ingestion
5. Elasticsearch stores logs
6. Kibana analyzes logs
7. Detection rules trigger alerts
8. Dashboards visualize activity

---

## 🎯 Project Outcome

- Successfully monitored Windows PowerShell activity
- Detected real-world attack techniques
- Generated alerts using custom rules
- Built a functional host-based SIEM detection pipeline
- Gained hands-on experience in detection engineering

---

## 🚀 Future Enhancements

- MITRE ATT&CK technique mapping
- Threat intelligence enrichment
- Automated response playbooks
- Additional Windows attack detections
- Multi-host monitoring

---

## ✅ Conclusion

This project demonstrates a practical implementation of Windows threat detection using the Elastic Stack. It closely mirrors real SOC workflows and provides a strong foundation for advanced detection engineering and threat intelligence projects.

---
