### 🔐 **Introduction To System/Host Based Attacks**

**Overview:**  
Attacks that directly target the operating system or applications running on a host. These can include privilege escalation, credential dumping, file system tampering, and persistence mechanisms.

**Key Concepts:**

- Initial access → Execution → Persistence → Privilege Escalation → Credential Access → Lateral Movement
    
- System hardening (e.g., disabling services, patching, reducing privileges)
    

**Tools to Know:**

- Metasploit, Empire, CrackMapExec
    

---

### 🪟 **Overview Of Windows Vulnerabilities**

**Overview:**  
Windows OS is a common target due to its market share and complexity. Vulnerabilities include misconfigurations, outdated patches, weak ACLs, and flawed services.

**Examples:**

- EternalBlue (SMBv1), PrintNightmare (spooler), CVE-2020-1472 (Zerologon)
    
- Misconfigured GPOs, unrestricted service permissions
    

**Real-World Use:**  
Look for these in unpatched enterprise environments, weak segmentation, or misconfigured AD setups.

---

### 🧨 **Exploiting Windows Vulnerabilities**

**Focus Areas:**

- Kernel and userland exploitation (e.g., CVE-2021-1732)
    
- Remote code execution (SMB, RDP, IIS)
    
- Local privilege escalation via services or DLL hijacking
    

**Tools:**

- Metasploit, Cobalt Strike, SharpHound, Mimikatz
    

---

### 🚀 **Windows Privilege Escalation**

**Overview:**  
Gaining SYSTEM or Admin privileges from a lower-privileged user.

**TTPs:**

- Insecure service permissions (e.g., `sc qc` to check)
    
- AlwaysInstallElevated MSI abuse
    
- Token impersonation
    
- Unquoted service paths
    

**Tools:**

- PowerUp, WinPEAS, Seatbelt, AccessChk
    

---

### 📁 **Windows File System Vulnerabilities**

**Concept:**  
Misconfigured file/folder permissions can allow attackers to overwrite or execute arbitrary code.

**Abuses:**

- Writable `C:\Program Files\` subdirs
    
- DLL search order hijacking
    
- NTFS alternate data streams
    

**Detection Tip:**  
Look for unexpected `.exe`, `.dll`, or hidden ADS (`file.txt:hidden.exe`)

---

### 🪪 **Windows Credential Dumping**

**Methods:**

- LSASS memory (via Mimikatz, Pypykatz)
    
- SAM registry hive (`reg save`, `secretsdump.py`)
    
- Token stealing, WDigest, LSA Secrets
    

**Post-Compromise Goal:**  
Use credentials for **lateral movement** or **persistence** (golden tickets, pass-the-hash).

---

### 🌐 **Windows Lateral Movement**

**Techniques:**

- PS Remoting, WMI, RDP, SMB sessions
    
- Pass-the-Hash, Pass-the-Ticket
    
- Admin shares (C$, ADMIN$)
    

**Tools:**

- CrackMapExec, Impacket, SharpRDP, PSExec
    

---

### 🐧 **Overview Of Linux Vulnerabilities**

**Common Issues:**

- SUID binaries
    
- Kernel exploits (e.g., Dirty COW)
    
- Weak file permissions (`/etc/shadow`, `cron` jobs)
    
- Exposed services (SSH, NFS, FTP, etc.)
    

**Real Targets:**

- Misconfigured web servers
    
- Weak SSH keys
    
- Forgotten scripts in cron
    

---

### 🧨 **Exploiting Linux Vulnerabilities**

**Focus Areas:**

- Local privilege escalation (e.g., GTFOBins)
    
- Exploiting weak configurations or SUID files
    
- Command injection, insecure daemons
    

**Tools:**

- LinPEAS, pspy, exploit-db
    

---

### 🚀 **Linux Privilege Escalation**

**Paths to Root:**

- Exploiting `sudo` misconfig (`sudo -l`)
    
- Writable cron jobs, PATH hijacks
    
- Kernel exploits
    

**Checklist:**

- `whoami`, `id`, `sudo -l`, `ls -la /etc/cron*`, `find / -perm -4000`
    

---

### 📁 **Linux File System Vulnerabilities**

**Focus:**  
Weak file permissions, exposed backups, world-writable files

**Examples:**

- `~/.bash_history`, `/etc/shadow`, log files, temp file races
    
- LFI/RFI via web apps (if hosted locally)
    

---

### 🪪 **Linux Credential Dumping**

**Methods:**

- `/etc/shadow` brute-force with John or Hashcat
    
- SSH key harvesting
    
- `ps aux` to find passwords in arguments
    
- `strings` or `grep` through config files (e.g., MySQL creds)
    

---

### 🔧 Lab Suggestions:

Set up a vulnerable lab using:

- **Windows Server + Windows 10/11** (Try HackTheBox, VulnHub, or manual builds)
    
- **Kali + Ubuntu/Debian/Arch**
    
- AD Domain setup with misconfigurations
    

Try tools like:

- **Responder** for NTLM poisoning
    
- **BloodHound** for AD mapping
    
- **LinEnum/WinPEAS** for enumeration

