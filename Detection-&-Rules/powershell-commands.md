# 🔍 PowerShell Commands Used – Explanation & Host Impact

This section explains the PowerShell and Windows commands used in the project, focusing on what each command does and how it affects the system host. These commands collectively simulate real-world attacker behavior commonly detected in SOC environments.

---

### 1️⃣ `powershell -EncodedCommand SQBFAFgA`
This command attempts to execute a Base64-encoded PowerShell payload. It spawns a PowerShell process even if the encoded string is invalid or incomplete. The execution attempt is logged in PowerShell operational logs. Attackers use this technique to obfuscate command content.

---

### 2️⃣ `$cmd = "Get-Process"`
This assigns the `Get-Process` command to a PowerShell variable. It does not execute the command or modify the system. The value exists only in memory during the session. Attackers often stage commands this way before encoding.

---

### 3️⃣ `[Convert]::ToBase64String([Text.Encoding]::Unicode.GetBytes($cmd))`
This converts the PowerShell command into a Base64-encoded Unicode string. No system changes occur, but an obfuscated payload is created. The encoded output is later used with `-EncodedCommand`. This is a common technique in fileless malware.

---

### 4️⃣ `powershell -NoProfile -ExecutionPolicy Bypass -EncodedCommand RwBlAHQALQBQAHIAbwBjAGUAcwBzAA==`
This launches PowerShell while bypassing execution policy restrictions. The encoded command is decoded and executed directly in memory. Skipping profiles reduces startup traces. This behavior is considered high-risk and strongly malicious.

---

### 5️⃣ `certutil -urlcache -split -f https://example.com test.txt`
This uses the built-in Windows `certutil` tool to download a file. It creates an outbound network connection and writes data to disk. Attackers abuse `certutil` as a Living-off-the-Land binary (LoLBin). It is commonly used to download malware payloads.

---

### 6️⃣ `Get-Process`
This command lists all currently running processes on the system. It does not alter the system or require elevated privileges. Attackers use it for reconnaissance to identify security tools. It helps plan further attack actions.

---

### 7️⃣ `powershell -ExecutionPolicy Bypass -NoProfile -c "whoami"`
This executes the `whoami` command through PowerShell. It reveals the current user and privilege context. No system modification occurs. Attackers use it to confirm their access level.

---

### 8️⃣ `powershell -NoProfile -WindowStyle Hidden -c "whoami"`
This runs PowerShell with the console window hidden. The command executes without visible user interaction. This stealth technique hides activity from the user. It is commonly used by malware for silent execution.

---

### 9️⃣ `cmd.exe /c powershell.exe -nop -c "whoami"`
This launches PowerShell from Command Prompt. It creates a suspicious parent-child process chain (`cmd.exe → powershell.exe`). Attackers use this to chain execution stages. SOC systems flag this as abnormal behavior.

---

### 🔟 `powershell -EncodedCommand RwBlAHQALQBQAHIAbwBjAGUAcwBzAA==`
This executes the Base64-encoded version of `Get-Process`. The payload is decoded and executed fully in memory. It performs process enumeration in an obfuscated way. This combination of encoding and execution is highly suspicious.

---

## 🎯 Final Summary
Individually, some of these commands may appear benign. However, when observed together, they form a clear PowerShell-based attack pattern involving obfuscation, execution policy bypass, stealth execution, reconnaissance, and Living-off-the-Land abuse. This behavior closely mirrors real-world PowerShell attacks monitored and detected by modern SOC and SIEM platforms.

