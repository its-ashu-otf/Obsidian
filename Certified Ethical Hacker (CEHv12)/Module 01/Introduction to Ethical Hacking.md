![[Module - 01 - Introduction to Ethical Hacking.pdf]]

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