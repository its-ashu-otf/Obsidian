To install **Apache2** and **Snort** on **Ubuntu Server 24.04 LTS**, follow the steps below. These instructions assume you're running as a user with `sudo` privileges.

---

## ✅ 1. Update System

```bash
sudo apt update && sudo apt upgrade -y
```

---

## 🌐 2. Install Apache2 Web Server

```bash
sudo apt install apache2 -y
```

### Check if it's running:

```bash
sudo systemctl status apache2
```

### Allow in UFW (optional):

```bash
sudo ufw allow 'Apache Full'
```

### Test:

Open your browser and go to `http://<your-server-ip>`. You should see the default Apache page.

---

## 🛡️ 3. Install Snort (IDS)

Snort is not in the default apt repos in its latest form, but you can install a working version with basic functionality directly via apt, or build from source if you need full customization.

### ⚡ Option A: Install Snort via apt (simpler, quicker)

```bash
sudo apt install snort -y
```

> During the install, it will ask for the network interface. For most setups, it's `ens33`, `eth0`, or `enp0s3`. You can check your interface with:

```bash
ip a
```

If you skipped configuration, run:

```bash
sudo dpkg-reconfigure snort
```

### ⚙️ Option B: (Advanced) Install Snort from Source (Latest Version)

If you want the latest Snort 3:

#### 1. Install dependencies:

```bash
sudo apt install -y build-essential libpcap-dev libpcre3-dev libdumbnet-dev \
bison flex zlib1g-dev liblzma-dev openssl libssl-dev \
libnghttp2-dev libdnet libdnet-dev autotools-dev \
cmake pkg-config libhwloc-dev libluajit-5.1-dev libpcap0.8-dev
```

#### 2. Install DAQ:

```bash
cd /tmp
wget https://www.snort.org/downloads/snort/daq-2.0.7.tar.gz
tar -xvzf daq-2.0.7.tar.gz
cd daq-2.0.7
./configure && make && sudo make install
```

#### 3. Install Snort 3:

```bash
cd /tmp
wget https://www.snort.org/downloads/snort/snort3-3.1.68.0.tar.gz
tar -xvzf snort3-3.1.68.0.tar.gz
cd snort3-3.1.68.0
./configure_cmake.sh --prefix=/usr/local --enable-tcmalloc
cd build
make -j$(nproc)
sudo make install
```

#### 4. Test:

```bash
snort -V
```

---

## 📂 4. Configure Snort (basic test mode)

Check interface name first:

```bash
ip a
```

Run Snort in test mode (replace `eth0` if needed):

```bash
sudo snort -i eth0 -A console -c /etc/snort/snort.conf -T
```

If successful, you’ll see:

```
Snort successfully validated the configuration!
Snort exiting
```

---

## 🧪 5. Run Snort in live mode (alert)

```bash
sudo snort -i eth0 -A console -c /etc/snort/snort.conf
```

It will now output alerts to the terminal for detected traffic.

---

## 🗂 Logs

- **Apache logs**: `/var/log/apache2/`
    
- **Snort alerts**: Usually in `/var/log/snort/alert`
    

---

Let me know if you want Snort configured with PulledPork or Snort3 rules, or integrated into your SIEM setup.