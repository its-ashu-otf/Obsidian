![[Pasted image 20250607232917.png]]


# 🔍 Alternate Data Streams (ADS) – NTFS Feature & Abuse

#### 🧠 **What is ADS?**

- **Alternate Data Streams (ADS)** are a feature of the **NTFS** (New Technology File System) in Windows.
    
- Originally implemented to ensure **compatibility with Mac’s HFS (Hierarchical File System)**, which supports multiple data "forks".
    
- NTFS allows files to contain multiple data streams beyond the primary one.
    

#### 📦 **Streams in a File:**

When a file is created on NTFS, it inherently supports:

1. **Data Stream** –  
    The default or primary stream containing the actual file content (what users normally interact with).
    
2. **Resource Stream** (Alternate Stream) –  
    An optional stream, usually hidden, used for metadata or auxiliary information (used by macOS originally).
    

---

### 🛠 **How ADS Can Be Used (or Abused):**

#### 🧨 **By Attackers:**

- Attackers **embed malicious code, scripts, or executables** into the alternate stream of a **legitimate-looking file**.
    
- This **hides malicious payloads** without visibly altering the file content or its size from a user’s perspective.
    
- Exploits the fact that **most file browsers, AV tools, and file size indicators ignore ADS**.
    

#### 📁 **Example of Creating ADS (cmd):**

```bash
echo MaliciousCode > normalfile.txt:evil.exe
```

This creates an alternate stream `evil.exe` attached to `normalfile.txt`.

To execute it (only works with certain interpreters or custom droppers):

```bash
start .\normalfile.txt:evil.exe
```

---

### 🎯 **Purpose in Attacks:**

- **Persistence**: Hide malware in system files to avoid detection.
    
- **Evasion**: Bypass **signature-based AVs**, basic **forensic tools**, and **file integrity monitors** that don't inspect ADS.
    
- **Stealth**: ADS do not change the **visible size or behavior** of a file unless the alternate stream is explicitly accessed.
    

---

### 🛡 **Detection and Defense:**

#### 🧰 **Tools:**

- **Sysinternals `streams.exe`**:
    
    ```bash
    streams.exe -s C:\path\
    ```
    
- **PowerShell**:
    
    ```powershell
    Get-Item -Path .\file.txt -Stream *
    ```
    

#### 🧱 **Mitigation:**

- **Regularly scan for alternate streams**.
    
- **Use EDR tools** that are capable of parsing and analyzing ADS.
    
- Disable ADS where possible using **group policies or file system restrictions**, though not always practical.


---

