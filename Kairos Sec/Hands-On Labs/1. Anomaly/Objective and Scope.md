

#### Objective

The core objective is to demonstrate the full impact of a successful network intrusion by achieving **Domain Administrator** privileges over the client's Active Directory environment. The test will simulate a motivated external attacker's progression from an initial foothold to complete administrative control.

#### Scope

The in-scope assets for this engagement include **two critical IP addresses**:

1. A hardened **Ubuntu Server** (Initial Foothold Target).
2. The primary **Domain Controller** (Final Privilege Escalation Target).

It is a critical finding that the **Domain Controller is running active Antivirus (AV) software**; therefore, this test will specifically involve techniques to **bypass or evade the installed AV** to successfully compromise the domain and demonstrate the potential for a full domain compromise.