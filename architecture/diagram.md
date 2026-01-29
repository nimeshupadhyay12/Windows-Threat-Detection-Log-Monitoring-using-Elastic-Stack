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
