# Requirements

##### 1. Vulnerable Web Application: https://phpgurukul.com/user-registration-login-and-user-management-system-with-admin-panel/
##### 2. Ubuntu-Server-VM ISO: https://ubuntu.com/download/server
##### 3. Patience 

# Setup Process

## VM Setup

1. After Downloading the ISO file, Open VMware Workstation and click this option **Create a New Virtual Machine** .

	![[Pasted image 20250531235347.png]]

2. Select **Typical** and move forward.
 
	 ![[Pasted image 20250531235448.png]]
3. Select the **ISO** file and click **Next**.

	![[Pasted image 20250531235555.png]]

4. Select the location to keep your Virtual Machine in and move forward

	![[Pasted image 20250531235617.png]]
5. Now, for the time of storage minimum 20 gb is good but i can spare some more, So i will give it 64gb 
	![[Pasted image 20250531235805.png]]

and move forward.
6. Now click the **Finish** button.

7. Make sure to disable the **Accelerate 3D graphics** as it will cause our VM to degrade our performance.
	![[Pasted image 20250531235911.png]]
8. **[Optional]** Recommended Advance Settings for Good experience

	![[Pasted image 20250601000216.png]]

9. Let's boot our VM
10. Booted in our VM, We are on setup. Let's glide through the setup hitting next on every prompt.
	![[Pasted image 20250601000342.png]]
11. Just hit the down arrow key and hit done as we will use entire disk
	![[Pasted image 20250601000515.png]]
12. Enter all the following in the setup.
	![[Pasted image 20250601000624.png]]
13. Setup SSH on this VM By hitting space key to select and the hit the down arrow key on done
	![[Pasted image 20250601000722.png]]
14. Now, Our Ubuntu Server VM Will start Installing.
15. After Installing Hit **Reboot Now**.
	![[Pasted image 20250601000904.png]]
16. You will probably get this error, Don't worry it's a easy fix we need to unmount the ISO File 
	![[Pasted image 20250601000946.png]]
17. Right click the ubuntu vm and open Settings.
	![[Pasted image 20250601001029.png]]
18. Select **CD/DVD** and git the remove button and then hit ok. 
	![[Pasted image 20250601001107.png]]
19. Now back in our ubuntu vm hit enter to reboot

![[Pasted image 20250601001220.png]]
and Just like that our vm should boot

20. Done !
![[Pasted image 20250601001334.png]]

<h2><centre>Congratulations ! You just installed ubuntu-server in a Virtual Machine.</centre> </h2>

## Vulnerable Web Application Setup

###  Prepping our VM (Installing Dependencies)

### 1. Install Apache

```bash
sudo apt update
sudo apt install apache2 -y
```

### 2. Install MySQL

```bash
sudo apt install mysql-server -y
```

### 3. Install PHP and Required Modules

```bash
sudo apt install php libapache2-mod-php php-mysql php-cli php-curl php-zip php-mbstring php-xml php-gd -y
```

---

## 📦 Step 2: Download and Configure the Project

### 1. Download the ZIP File

If you have it locally, move it to your server, or download it via terminal:

```bash
wget https://some-url-to-your-project.zip -O loginsystem.zip
```

_(Replace the above URL with the real one or upload it via SCP or SFTP if you're hosting it yourself)_

### 2. Extract and Move Project Files

```bash
unzip loginsystem.zip
sudo mv loginsystem /var/www/html/
sudo chown -R www-data:www-data /var/www/html/loginsystem
sudo chmod -R 755 /var/www/html/loginsystem
```

---

## 🛠 Step 3: Configure MySQL Database

### 1. Login to MySQL

```bash
sudo mysql -u root -p
```

### 2. Create Database and Import SQL

```sql
CREATE DATABASE loginsystem;
USE loginsystem;
SOURCE /var/www/html/loginsystem/SQL/loginsystem.sql;
EXIT;
```

_(Adjust the `.sql` path based on actual location inside the extracted project)_

---

## 🛠 Step 4:  Install PHPMyAdmin**

Ensure PHPMyAdmin is installed:

```bash
sudo apt install phpmyadmin php-mbstring php-zip php-gd php-json php-curl -y
sudo phpenmod mysqli mbstring
sudo systemctl restart apache2
```

While installing prompt **yes** for password and set a password something rememberable.

![[Pasted image 20250601003118.png]]

## ## 🛠 Step 5:  Allow No Password Logins

If you're only testing locally and absolutely must allow logins **without** a password (NOT RECOMMENDED):

1. Edit the MySQL config (usually `/etc/mysql/mariadb.conf.d/50-server.cnf` or `/etc/mysql/mysql.conf.d/mysqld.cnf`):
    

```bash
sudo nano /etc/mysql/mysql.conf.d/mysqld.cnf
```

2. Under `[mysqld]`, **add or update**:
    

```ini
[mysqld]
skip-grant-tables
```

![[Pasted image 20250601003406.png]]

3. Restart MySQL:
    

```bash
sudo systemctl restart mysql
```

> ⚠️ This disables _all_ authentication — **don’t do this unless it’s a controlled lab**.

---

## 🛠 Step 6:  Access phpMyAdmin

![[Pasted image 20250601003609.png]]

Use default credentials 

**Username:** `admin`
**Password:**`password`

and login.

**Let's confirm our databases is successfully imported or not.** 

![[Pasted image 20250601003735.png]]

our databases is present 

Let's now check our vulnerable application


## 🛠 Step 7: Access the vulnerable application

Open up your browser and access this. 

```http
http://<ubuntu-server-ip>/loginsystem/
```

![[Pasted image 20250601003913.png]]

Login page works too.

![[Pasted image 20250601004127.png]]

Let's trying logging in normally. 

```
For admin Panel http://localhost/loginsystem/admin  
Credential for admin panel :  
Username: admin  
Password: Test@12345  
Credential for user panel :  
Username: johndoe12@gamil.com  
Password : Test@123
```

Done ! 

