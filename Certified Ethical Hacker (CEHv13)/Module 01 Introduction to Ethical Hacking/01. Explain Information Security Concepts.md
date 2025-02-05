# Information Security Overview
**Information Security** refers to the practice of defending information from unauthorized access, use, disclosure, disruption, modification, or destruction."

This definition encompasses various aspects of protecting digital assets, including the **CIA Triad** and Other Elements too:

![[Pasted image 20241106151029.jpg]]

1. **Confidentiality (C):**
    - Protecting sensitive information from unauthorized access.
    - Ensuring that only authorized personnel can view or use sensitive data.
2. **Integrity (I):**
    - Ensuring that data is accurate, complete, and not modified by unauthorized parties.
    - Preventing tampering or alteration of data during transmission or storage.
3. **Availability (A):**
    - Making sure that data and systems are accessible when needed.
    - Ensuring that authorized personnel can access necessary resources and information.
4. **Authenticity:** 
	- Ensures the message comes from a specific sender. 
	- Guarantees the message is genuine and has not been altered.   
 1. **Non-Repudiation:**
	*  Ensures the sender cannot deny sending a message.
	*  Holds the sender accountable for their actions.

The primary goal of Information Security is to ensure the confidentiality, integrity, and availability of information, as well as protecting it from cyber threats and risks.

## Motives, Goals, and Objectives  Of Information Security Attacks
## <centre> <span style="color:rgb(255, 0, 0)"><b>Attacks</b></span> <span style="color:rgb(0, 0, 0)">= <b>Motive(Goal) + Method + Vulnerability</b></span> </centre>

### Attack Formula
An **attack** is defined as a combination of:
- **Motive (Goal)**: The reason for the attack, which usually arises from the attacker’s belief that the target system or data has value.
- **Method**: The technique or tool used to carry out the attack.
- **Vulnerability**: A weakness in the system or security policies that attackers exploit to achieve their goals.

### Motives Behind Attacks
The image lists various motives that drive attackers:
- **Disrupting Business Continuity**: Causing interruptions to a business's operations.
- **Stealing Information and Manipulating Data**: Accessing or altering sensitive data.
- **Creating Fear and Chaos by Disrupting Critical Infrastructures**: Targeting essential services (like power or transportation) to instil fear.
- **Causing Financial Loss**: Leading to direct or indirect financial harm to the target.
- **Propagating Religious or Political Beliefs**: Using attacks as a means to promote certain ideologies.
- **Achieving Military Objectives**: Conducting attacks to fulfil a nation-state’s strategic or military goals.
- **Damaging the Target's Reputation**: Tarnishing the target's public image.
- **Taking Revenge**: Personal or organizational retaliation.
- **Demanding Ransom**: Requiring payment (often through ransomware) to restore access to data or systems. 

This framework helps understand that information security attacks are usually intentional actions with specific goals, carried out by leveraging weaknesses in systems.

### Classifications Of Attacks
The image categorizes types of information security attacks, providing examples for each type:

### 1. Passive Attacks
These attacks focus on **monitoring and intercepting** network traffic without altering any data. The goal is to gather information covertly.
- **Examples**:
  - **Sniffing**: Capturing data packets traveling across a network, often to collect sensitive information like passwords.
  - **Eavesdropping**: Listening in on private conversations or data exchanges to collect confidential information.

### 2. Active Attacks
Active attacks involve **tampering with data in transit or disrupting communication** between systems to compromise security.
- **Examples**:
  - **Denial of Service (DoS)**: Overloading a server or network to make it unavailable to users.
  - **Man-in-the-Middle (MitM)**: Intercepting and potentially altering communications between two parties without their knowledge.
  - **Session Hijacking**: Taking over a user's session, often by stealing session tokens, to gain unauthorized access.
  - **SQL Injection**: Injecting malicious SQL code into a database query to manipulate or retrieve unauthorized data.
  - **Phishing and Spear Phishing**:  Deceptive messages trick users into revealing sensitive information or clicking on malicious links.
  - **Ransomware Attacks**: Malware encrypts data and demands a ransom to restore access.
  - **Cross-Site Scripting (XSS)**: Malicious scripts are injected into trusted websites, executed in users' browsers.
  - **Cross-Site Request Forgery (CSRF)**:  Tricks users into performing unintended actions on a trusted site where they are authenticated.
  - **Brute Force Attacks**: Systematically guesses login credentials by trying all possible combinations.
 - **Password Spraying**: Tries common passwords across a large number of accounts to exploit weak or default passwords.
  - **DNS Spoofing (Cache Poisoning)**: Alters DNS records to redirect users to malicious sites that mimic legitimate ones.
  - **Distributed Denial of Service (DDoS)**:  Multiple systems flood a target with traffic, rendering it unusable.
  - **Remote Code Execution (RCE)**: Executes malicious code on a target server or device, providing control over the system.
  - **ARP Spoofing**: Tricks a network into associating the attacker’s MAC address with another device’s IP address.
  - **Botnets and Command-and-Control (C&C) Attacks**: A network of infected devices is remotely controlled to conduct large-scale attacks.

### 3. Close-in Attacks
Close-in attacks require the attacker to be in **close physical proximity** to the target system. They often use social engineering to gain access to restricted areas.
- **Examples**:
  - **Social Engineering**: Tricking employees into revealing information or allowing access.
  - **Shoulder Surfing**: Watching over someone's shoulder to see passwords or other sensitive information.
  - **Dumpster Diving**: Searching through trash to find confidential information like discarded documents with sensitive data.

### 4. Insider Attacks
These attacks are carried out by individuals with **privileged access** within the organization, either intentionally or due to negligence. 
- **Examples**:
  - **Theft of Physical Devices**: Taking laptops, USB drives, or other devices that contain sensitive data.
  - **Planting Keyloggers**: Installing software or hardware to record keystrokes and gather information like passwords.
  - **Using Backdoors and Malware**: Installing backdoors or malware to gain unauthorized access.

### 5. Distribution Attacks
Distribution attacks occur when attackers **tamper with hardware or software** during its manufacturing or distribution phase, making it compromised before it reaches the end user.
- **Examples**:
  - **Hardware Tampering**: Adding malicious chips to hardware during manufacturing, which can enable unauthorized access or data leakage.
  - **Software Tampering**: Modifying software or firmware updates to include malware, which can infect systems upon installation.

## Tactics, Techniques, and Procedures (TTPs)

**Tactics, Techniques, and Procedures (TTPs)** are critical components in understanding and analyzing the behavior of adversaries in cybersecurity. This framework is part of threat intelligence and helps security professionals understand how attackers operate. 

Here’s an elaboration of TTPs:

---

### **1. Tactics**

- **Definition**: Tactics refer to the high-level objectives or goals of the adversary during an attack. These goals often align with the stages of the Cyber Kill Chain or MITRE ATT&CK Framework.
    
- **Common Tactics in CEH Context**:
    
    1. **Initial Access**: Methods to gain entry into the target environment.
        - Example: Spear-phishing emails, exploiting vulnerabilities, or brute-forcing login credentials.
    2. **Persistence**: Techniques to maintain access over time, even after reboots or detection.
        - Example: Installing backdoors or using scheduled tasks.
    3. **Privilege Escalation**: Moving from low-privileged access to higher privileges.
        - Example: Exploiting misconfigured SUID binaries in Linux.
    4. **Defence Evasion**: Techniques to bypass security mechanisms.
        - Example: Encrypting payloads to bypass antivirus detection.
    5. **Credential Access**: Harvesting passwords or authentication tokens.
        - Example: Using tools like _Mimikatz_ to extract credentials from Windows memory.
    6. **Exfiltration**: Transferring stolen data to the attacker’s system.
        - Example: Using _Rclone_ to upload data to cloud storage.

---

### **2. Techniques**

- **Definition**: Techniques are the specific methods or processes attackers use to achieve their tactics. Each tactic can have multiple techniques.
    
- **Examples of Techniques in CEH Context**:
    
    1. **Phishing (Initial Access)**:
        - Crafting emails with malicious links or attachments that trick users into opening them.
        - Example: Using _SET (Social-Engineer Toolkit)_ to send convincing phishing emails.
    2. **Exploiting Software Vulnerabilities (Initial Access)**:
        - Exploiting known vulnerabilities like _CVE-2017-0144_ (EternalBlue) to compromise systems.
    3. **DLL Injection (Defense Evasion)**:
        - Injecting malicious code into legitimate processes to evade detection.
        - Example: Using Metasploit’s _DLL injection module_.
    4. **Credential Dumping (Credential Access)**:
        - Extracting passwords from SAM (Security Account Manager) files on Windows systems.
        - Example: Tools like _Mimikatz_ or _LaZagne_.
    5. **Command and Control via DNS Tunneling (Command and Control)**:
        - Sending encoded messages over DNS queries to communicate with a remote server.
        - Example: Using tools like _Iodine_.

---

### **3. Procedures**

- **Definition**: Procedures are the detailed steps or workflows attackers follow to implement techniques. Procedures vary between adversaries depending on their expertise, resources, and objectives.
    
- **Examples of Procedures in CEH Context**:
    
    1. **Phishing Workflow**:
        - **Step 1**: Create a phishing email with a malicious attachment (e.g., a Word file with macros).
        - **Step 2**: Use tools like _Gophish_ to send bulk phishing emails.
        - **Step 3**: Harvest credentials or install malware when the user opens the attachment.
    2. **Privilege Escalation Workflow**:
        - **Step 1**: Identify misconfigured permissions or vulnerable applications (e.g., unpatched sudo).
        - **Step 2**: Exploit the identified vulnerability to gain administrative access.
    3. **Data Exfiltration Workflow**:
        - **Step 1**: Compress sensitive files using tools like _7zip_ or _WinRAR_.
        - **Step 2**: Encrypt files to evade detection.
        - **Step 3**: Use _FTP_, _Rclone_, or HTTP POST requests to transfer data to a remote server.

---

### **TTPs in Practice: Attack Scenario**

#### **Example 1: Credential Dumping via Mimikatz**

- **Tactic**: Credential Access.
- **Technique**: Credential Dumping.
- **Procedure**:
    1. Use Mimikatz to dump plaintext passwords from LSASS memory.
    2. Authenticate with dumped credentials on other machines in the network.
    3. Maintain persistence by creating an administrative account with the stolen credentials.

#### **Example 2: Exploiting SMB Vulnerability**

- **Tactic**: Initial Access.
- **Technique**: Exploiting Unpatched Services.
- **Procedure**:
    1. Scan the network using _Nmap_ to identify SMB service running on Port 445.
    2. Confirm the presence of the EternalBlue vulnerability (CVE-2017-0144).
    3. Use Metasploit to launch the exploit and gain remote shell access.
    4. Deploy a backdoor for persistence.

---

### **Why TTPs Matter in CEH?**

Understanding TTPs helps ethical hackers:

- **Detect Threats**: By correlating TTPs to specific adversary behaviors (e.g., ransomware campaigns).
- **Mitigate Risks**: Identifying patterns in TTPs to predict and prevent future attacks.
- **Improve Incident Response**: Building defenses around known adversarial tactics and techniques.

### **Defensive Measures Against TTPs**

1. **Reconnaissance Prevention**:
    
    - Use anti-reconnaissance tools like _Snort_ to detect scanning activities.
    - Restrict information leakage via DNS, WHOIS, or social media.
2. **Exploitation Prevention**:
    
    - Regularly patch systems and applications.
    - Implement IDS/IPS solutions like _Suricata_ or _Zeek_.
3. **Credential Protection**:
    
    - Enforce multi-factor authentication (MFA).
    - Use tools like _LAPS_ (Local Administrator Password Solution) to manage local admin credentials securely.
4. **Command and Control Prevention**:
    
    - Monitor outbound traffic for anomalies.
    - Block known C2 domains using threat intelligence feeds.

---

This structured understanding of **TTPs** equips ethical hackers with tools and techniques to effectively counteract cyber threats. Let me know if you’d like more real-world scenarios or tool recommendations!

## Vulnerability
A **vulnerability**  is defined as a **weakness in a system, application, network, or process that can be exploited by a threat actor to gain unauthorized access, compromise confidentiality, integrity, or availability, or disrupt normal operations**. Vulnerabilities can exist in hardware, software, configurations, or even in organizational processes.

### Common Reasons for Vulnerabilities

1. **Hardware or Software Misconfiguration**
    
    - **Cause:** Misconfigured settings, such as unencrypted protocols or poorly secured devices, lead to exploitable loopholes.
    - **Impact:** Attackers can gain unauthorized access to systems, steal data, or disrupt operations.
    - **Example:** Leaving default admin credentials active or failing to disable unnecessary services.
2. **Insecure or Poor Design of Networks and Applications**
    
    - **Cause:** Networks and applications designed without considering security can expose attack surfaces.
    - **Impact:** Threats such as data breaches or network compromise become more likely.
    - **Example:** Improperly configured firewalls, lack of segmentation, or weak VPN setups.
3. **Inherent Technology Weaknesses**
    
    - **Cause:** Flaws or limitations in hardware or software that cannot adequately defend against specific threats.
    - **Impact:** Systems become vulnerable to targeted attacks such as **DoS**, **Man-in-the-Middle (MitM)**, or exploitation of outdated components.
    - **Example:** Systems running outdated browsers or unsupported OS versions are prone to exploitation.
4. **End-User Carelessness**
    
    - **Cause:** Human error or negligence, such as sharing credentials, using weak passwords, or falling victim to phishing attacks.
    - **Impact:** Unauthorized access, data breaches, or malware infections.
    - **Example:** A user clicking on a malicious link in a phishing email or connecting to unsecured public Wi-Fi.
5. **Intentional End-User Acts**
    
    - **Cause:** Malicious actions by insiders (e.g., disgruntled employees) or ex-employees who retain unauthorized access.
    - **Impact:** Loss of sensitive data, intellectual property theft, or financial damage.
    - **Example:** An ex-employee intentionally leaking sensitive company documents.

Here’s a summary and breakdown of the **examples of technological and configuration vulnerabilities** :

---

### **Technological Vulnerabilities**

These vulnerabilities arise due to inherent weaknesses in technology and protocols:

|**Type**|**Description**|
|---|---|
|**TCP/IP Protocol Vulnerabilities**|Protocols such as HTTP, FTP, ICMP, SNMP, and SMTP are inherently insecure and lack robust security mechanisms.|
|**Operating System Vulnerabilities**|- Inherently insecure design or architecture. - Lack of regular updates or patches to fix known issues.|
|**Network Device Vulnerabilities**|- Lack of password protection or weak passwords. - No authentication mechanisms for access. - Use of insecure routing protocols. - Vulnerabilities in firewall configurations.|

---

### **Configuration Vulnerabilities**

These vulnerabilities are caused by improper configuration or lack of attention to security details:

|**Type**|**Description**|
|---|---|
|**User Account Vulnerabilities**|Occur due to insecure transmission of credentials (e.g., usernames and passwords) over the network, leading to credential theft.|
|**System Account Vulnerabilities**|Weak or easily guessable passwords for system accounts increase the risk of unauthorized access.|
|**Internet Service Misconfiguration**|Enabling features or misconfiguring services like IIS, Apache, FTP, or terminal services can create security loopholes. For instance, enabling JavaScript without restrictions.|
|**Default Passwords and Settings**|Leaving devices or systems with factory default passwords or configurations provides attackers with an easy entry point.|
|**Network Device Misconfiguration**|Misconfigured routers, firewalls, or switches can expose the network to unauthorized access or data leaks.|

---

### **Key Takeaways**

1. **Technological Vulnerabilities** often require software updates, patches, or the replacement of outdated technologies.
2. **Configuration Vulnerabilities** can be mitigated with proper configuration management, the use of strong passwords, and avoiding the use of default settings.
3. Vulnerabilities are caused by a combination of technical and human factors. Regular security assessments, proper configurations, user training, and robust access control policies are essential to minimize these risks.

**Proactive Steps:** Regular vulnerability assessments, penetration testing, and secure configurations are essential to identifying and fixing these weaknesses.


## Information Warfare

**Information Warfare** (InfoWar), which is the use of information and communication technologies (ICT) to gain a competitive advantage over opponents. 

![[Pasted image 20241106155657.png]]

Information Warfare is divided into **Defensive** and **Offensive** approaches.
### Defensive Information Warfare

- Focuses on protecting ICT assets from attacks.
- Involves several strategies and actions, such as:
    - **Prevention**: Implementing measures to prevent attacks.
    - **Deterrence**: Discouraging attackers by making defences strong and visible.
    - **Alerts**: Setting up systems to provide warnings about potential threats.
    - **Detection**: Identifying attacks in progress or completed.
    - **Emergency Preparedness**: Preparing for quick responses in case of attacks.
    - **Response**: Taking actions to mitigate or stop attacks once detected.

### Offensive Information Warfare

- Focuses on attacking the ICT assets of an opponent.
- Involves various types of attacks, including:
    - **Web Application Attacks**: Targeting applications on the web, like SQL injection or XSS.
    - **Web Server Attacks**: Compromising web servers, often to disrupt services or steal data.
    - **Malware Attacks**: Deploying malicious software to damage or control opponent systems.
    - **MITM (Man-in-the-Middle) Attacks**: Intercepting communications between parties to steal or alter information.
    - **System Hacking**: Gaining unauthorized access to systems to exploit or control them.

Defensive warfare aims to secure and protect systems, while offensive warfare targets vulnerabilities in an opponent’s systems to gain an advantage.

**Martin Libicki**, a prominent researcher in information warfare, classified **Information Warfare (IW)** into seven distinct categories. Each type reflects different ways that information and technology can be used in conflict or competition. Here’s a summary of Libicki’s classification:

1. **Command and Control Warfare (C2W)**  
   - Focuses on disrupting or destroying an enemy's command and control systems to degrade their ability to make decisions.
   - Involves activities like psychological operations, electronic warfare, and deception to impair the adversary’s decision-making process.

2. **Intelligence-Based Warfare (IBW)**  
   - Involves gathering, analysing, and using intelligence to gain an advantage over opponents.
   - Uses advanced sensors, data processing, and surveillance to collect and exploit information about adversaries.

3. **Electronic Warfare (EW)**  
   - Utilizes electromagnetic spectrum (like radio, radar, or GPS) to disrupt enemy electronics and communications.
   - Includes jamming, electronic countermeasures, and anti-jamming efforts to control or deny the adversary’s access to the spectrum.

4. **Psychological Warfare (PsyOps)**  
   - Aims to influence the opinions, emotions, attitudes, and behaviour of adversaries.
   - Involves propaganda, misinformation, and other tactics to undermine morale, confuse, or create fear in the enemy.

5. **Hacker Warfare**  
   - Involves using computer hacking techniques to attack or defend information systems.
   - Includes activities like exploiting vulnerabilities, creating backdoors, and distributing malware to compromise or control systems.

6. **Economic Information Warfare**  
   - Focuses on attacking or manipulating an opponent's economy through cyber or information means.
   - Involves disrupting financial systems, stealing intellectual property, and causing economic damage by targeting critical infrastructure.

7. **Cyber Warfare**  
   - Encompasses a wide range of operations conducted in cyberspace to attack or defend networked systems.
   - Includes denial of service attacks, data breaches, and cyber espionage aimed at disrupting, damaging, or infiltrating networks.

Libicki’s classification provides a framework to understand the different dimensions of information warfare, each with unique tactics, targets, and objectives. These categories highlight the diverse methods by which information and technology are weaponized in modern conflicts.

Each form of information warfare mentioned above consists of both defensive and offensive
strategies.
- **Defensive Information Warfare:** Involves all strategies and actions to defend against
attacks on ICT assets.
- **Offensive Information Warfare:** Involves attacks against the ICT assets of an opponent.