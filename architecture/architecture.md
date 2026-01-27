# 🏗️ Architecture Overview

This document explains the architecture of the **Windows Threat Detection & Log Monitoring System** built using the Elastic Stack. The architecture is designed to simulate real-world SOC monitoring, where a Windows machine acts both as a **victim endpoint** and a **log source**, while Elastic Stack components function as the **SIEM platform**.

---

## 🖥️ Windows as Victim + SIEM Log Source

- The Windows machine plays a dual role:
  - **Victim Endpoint**:  
    - PowerShell commands (both benign and malicious) are executed on the system
    - These commands simulate attacker activity such as script execution, encoded commands, and LoLBins abuse
  - **Log Source for SIEM**:  
    - Windows generates telemetry including:
      - PowerShell execution logs
      - Security event logs
      - System logs
- These logs represent real-world endpoint activity typically monitored by SOC teams

---

## 🔗 Elastic Stack Data Flow

The data pipeline follows a structured and centralized SIEM architecture:

### Elastic Agent → Fleet → Elasticsearch → Kibana

### 1️⃣ Elastic Agent (On Windows Host)
- Installed directly on the Windows machine
- Responsible for collecting:
  - `windows.powershell`
  - `windows.security`
  - `windows.system`
- Captures:
  - Process creation
  - Command-line arguments
  - Execution metadata
- Sends logs securely to Fleet Server

---

### 2️⃣ Fleet Server (Central Management Layer)
- Acts as the control plane for all Elastic Agents
- Responsibilities:
  - Agent enrollment
  - Policy assignment
  - Integration management
- Ensures consistent log collection and configuration across endpoints

---

### 3️⃣ Elasticsearch (Storage & Search Engine)
- Receives logs from Fleet-managed agents
- Stores and indexes log data efficiently
- Enables:
  - Fast search
  - Correlation
  - Detection rule evaluation

---

### 4️⃣ Kibana (SIEM & Visualization Layer)
- Provides the user interface for security monitoring
- Used for:
  - Log analysis
  - Detection rule creation (KQL-based)
  - Alert generation
  - Dashboard visualization
- Serves as the SOC analyst’s primary investigation console

---

## ⚔️ PowerShell Execution as Attack Vector

- PowerShell is used as the primary **attack simulation vector**
- Simulated activities include:
  - Encoded PowerShell commands
  - Script-based execution
  - Suspicious command-line usage
- These techniques reflect:
  - Living-off-the-Land (LoLBins) attacks
  - Fileless malware behavior
  - Initial access and execution phases of real-world attacks
- Detection rules in Kibana are designed to identify these behaviors based on log telemetry

---


Attacker / User
      |
      v
PowerShell Command Execution
      |
      v
Windows Event Generation
(PowerShell, Security, System Logs)
      |
      v
Elastic Agent (Windows)
      |
      v
Fleet Server
(Agent & Policy Management)
      |
      v
Elasticsearch
(Log Storage & Indexing)
      |
      v
Kibana
(Log Analysis & Detection Rules)
      |
      v
Security Alerts & Dashboards
