```table-of-contents
```

## Pre-requisites
- **Kali-Linux** (Our Preferred Penetration Testing Distro)
- **Ubuntu-Server-VM**
	- Minimum 2 Cores & 2GB Ram
	- Storage: 20GB Minimum
- **Windows-Server-VM** (For this instance I'll be using Windows Server 2022)
- Internet Connection

## Setup on Ubuntu-Server

### Installing Wazuh

 1. Download and run the Wazuh installation assistant.
 ```bash
 curl -sO https://packages.wazuh.com/4.14/wazuh-install.sh && sudo bash ./wazuh-install.sh -a
 ```
 
Once the assistant finishes the installation, the output shows the access credentials and a message that confirms that the installation was successful.

```
INFO: --- Summary ---
INFO: You can access the web interface https://<WAZUH_DASHBOARD_IP_ADDRESS>
    User: admin
    Password: <ADMIN_PASSWORD>
INFO: Installation finished.
```

You now have installed and configured Wazuh.

2. Access the Wazuh web interface with `https://<WAZUH_DASHBOARD_IP_ADDRESS>` and your credentials:
    
    - **Username**: `admin`
        
    - **Password**: `<ADMIN_PASSWORD>`
        

When you access the Wazuh dashboard for the first time, the browser shows a warning message stating that the certificate was not issued by a trusted authority. This is expected and the user has the option to accept the certificate as an exception or, alternatively, configure the system to use a certificate from a trusted authority.

> [!NOTE] Note 
> You can find the passwords for all the Wazuh indexer and Wazuh API users in the `wazuh-passwords.txt` file inside `wazuh-install-files.tar`. To print them, run the following command:
>```bash
>$ sudo tar -O -xvf wazuh-install-files.tar wazuh-install-files/wazuh-passwords.txt
>```

If you want to uninstall the Wazuh central components, run the Wazuh installation assistant using the option `-u` or `–-uninstall`.

> [!NOTE] Note
>**Recommended Action**: Disable Wazuh Updates.
>We recommend disabling the Wazuh package repositories after installation to prevent accidental upgrades that could break the environment.
>Execute the following command to disable the Wazuh repository:
>```bash
>$ sed -i "s/^deb /#deb /" /etc/apt/sources.list.d/wazuh.list
>$ apt update
>```

#### Next steps

Now that your Wazuh installation is ready, you can start deploying the Wazuh agent. This can be used to protect laptops, desktops, servers, cloud instances, containers, or virtual machines. The agent is lightweight and multi-purpose, providing a variety of security capabilities.
### Deploying an Agent

