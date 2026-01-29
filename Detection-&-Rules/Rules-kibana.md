# 🔍 Kibana Detection Rules Explanation

This section explains the detection rules created in Kibana for identifying suspicious and malicious PowerShell activity on a Windows host. Each rule focuses on a specific behavioral pattern commonly observed in real-world attacks and SOC investigations.

---

## 🔹 Rule 1: PowerShell Hidden Window Execution
This rule detects PowerShell commands executed with a hidden window using flags such as `-WindowStyle Hidden`. Hidden execution prevents the user from seeing any console activity on the system. Attackers use this technique to run malicious scripts silently without raising user suspicion. It is a strong indicator of stealthy, fileless malware behavior.

---

## 🔹 Rule 2: Command Prompt Spawning PowerShell
This rule identifies scenarios where `cmd.exe` launches `powershell.exe`, creating a suspicious parent–child process relationship. Such behavior is uncommon during normal user activity. Attackers use this chaining technique to stage, automate, or deliver malicious payloads. SOC teams monitor this pattern as a reliable behavioral indicator of compromise.

---

## 🔹 Rule 3: PowerShell ExecutionPolicy Bypass
This rule detects PowerShell executions that use the `ExecutionPolicy Bypass` flag. This option allows scripts to run without restriction, ignoring system-defined PowerShell security policies. Attackers rely on this technique to execute malicious code on locked-down or hardened systems. This behavior is classified as high-risk in detection engineering.

---

## 🔹 Rule 4: PowerShell Encoded Command Execution
This rule identifies PowerShell commands executed using the `-EncodedCommand` flag. Encoded commands hide malicious intent through Base64 obfuscation, making analysis more difficult. This technique is commonly used in fileless attacks and malware loaders. Detection of encoded execution is considered a strong signal of malicious activity.

---
