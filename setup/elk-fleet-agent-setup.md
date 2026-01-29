# ⚙️ ELK + Fleet + Elastic Agent Setup (Short Guide)

This document provides a concise overview of how the **ELK Stack with Fleet Server and Elastic Agent** was configured for the  
**Windows Threat Detection & Log Monitoring** project.

---

## 📌 Objective
- Centralize Windows log collection
- Manage Elastic Agents using Fleet Server
- Collect PowerShell, Security, and System logs
- Enable detection engineering and alerting in Kibana

---

## 🧱 Components Used
- **Elasticsearch** – Log storage and indexing  
- **Kibana** – SIEM interface, detections, dashboards  
- **Fleet Server** – Centralized agent management  
- **Elastic Agent** – Windows log collection  
- **Windows OS** – Endpoint and telemetry source  

---

## 🏗️ Setup Steps

### 1️⃣ Install Elasticsearch & Kibana
- Install Elasticsearch and start the service  
- Install Kibana and start the service  
- Verify access:
  - `http://localhost:9200`
  - `http://localhost:5601`

---

### 2️⃣ Enable Fleet & Install Fleet Server
- Open **Kibana → Management → Fleet**
- Enable Fleet
- Install Fleet Server
- Confirm Fleet Server status shows **Healthy**

---

### 3️⃣ Create Agent Policy
- Create a Windows agent policy in Fleet
- Add **Windows integration**
- Enable:
  - PowerShell logs
  - Security logs
  - System logs
- Save the policy

---

### 4️⃣ Install Elastic Agent on Windows
- Go to **Fleet → Agents → Add Agent**
- Select Windows platform
- Choose the created agent policy
- Run the enrollment command in **PowerShell (Administrator)**

---

### 5️⃣ Verify Log Ingestion
In **Kibana → Discover**, verify logs using:
```kql
data_stream.dataset : "windows.powershell"
