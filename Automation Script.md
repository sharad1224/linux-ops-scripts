# linux-ops-scripts

## 🚀 Script: CPU info



#!/bin/bash
# This line tells the system to use Bash to run the script.

echo "Current CPU Load Average:"
uptime | awk -F'load average:' '{ print $2 }'



# Help with Shell script that monitors CPU Usage
#!/bin/ksh
top -b -n 1 |head -8 >/tmp/cpu.text
sed -e '1,5d' /tmp/cpu.text >/tmp/cpu2.text
High_CPU=`cat /tmp/cpu2.text|tail -1|awk '{print $9}'`
host=`hostname`
if [ "$High_CPU -gt  90" ];
then
mail -s "High CPU USAGE on $host" test@test.comv < /tmp/cpu2.lst
fi
exit;


# Linux Network Configuration Check Script

A **clean and practical Bash script** to verify **networking configuration on Linux systems**.  
Designed using **RHCSA best practices**, compatible with major Linux distributions.

---

## 📌 Features

The script performs the following checks:

- ✅ Network interfaces and link state
- ✅ IP address assignment
- ✅ Routing table and default gateway
- ✅ DNS configuration
- ✅ NetworkManager service status
- ✅ Connectivity tests (gateway & internet)
- ✅ DNS resolution test
- ✅ Listening network ports (basic)

---

## 🧾 Script: `network_check.sh`

```bash
#!/bin/bash
# ---------------------------------------------
# Network Configuration Check Script
# Author: Sharad Patel
# Description: Performs basic Linux networking checks
# ---------------------------------------------

echo "========================================="
echo " Linux Network Configuration Check"
echo "========================================="
echo

section() {
    echo
    echo "---- $1 ----"
}

section "Hostname"
hostnamectl

section "Network Interfaces (ip link)"
ip -br link show

section "IP Address Configuration"
ip -br addr show

section "NetworkManager Status"
if systemctl is-active NetworkManager &>/dev/null; then
    echo "NetworkManager is running"
    nmcli device status
else
    echo "NetworkManager is NOT running"
fi

section "Routing Table"
ip route show

DEFAULT_GW=$(ip route | awk '/default/ {print $3}')
if [[ -n "$DEFAULT_GW" ]]; then
    echo "Default Gateway: $DEFAULT_GW"
else
    echo "No default gateway configured"
fi

section "DNS Configuration"
if [[ -f /etc/resolv.conf ]]; then
    cat /etc/resolv.conf
else
    echo "/etc/resolv.conf not found"
fi

section "Connectivity Test"
echo "Pinging default gateway..."
ping -c 2 "$DEFAULT_GW" &>/dev/null && echo "Gateway reachable" || echo "Gateway NOT reachable"

echo "Pinging public DNS (8.8.8.8)..."
ping -c 2 8.8.8.8 &>/dev/null && echo "Internet connectivity OK" || echo "Internet connectivity FAILED"

section "DNS Resolution Test"
getent hosts google.com &>/dev/null && echo "DNS resolution working" || echo "DNS resolution failed"

section "Listening Network Ports"
ss -tulnp | head -20

echo
echo "========================================="
echo " Network Check Completed"
echo "========================================="






Below is a **ready-to-upload `README.md`** for your GitHub repository.
It’s clean, professional, and **RHCSA-aligned**, suitable for recruiters and technical reviewers.

---

````md
# Linux Network Configuration Check Script

A **clean and practical Bash script** to verify **networking configuration on Linux systems**.  
Designed using **RHCSA best practices**, compatible with major Linux distributions.

---

## 📌 Features

The script performs the following checks:

- ✅ Network interfaces and link state
- ✅ IP address assignment
- ✅ Routing table and default gateway
- ✅ DNS configuration
- ✅ NetworkManager service status
- ✅ Connectivity tests (gateway & internet)
- ✅ DNS resolution test
- ✅ Listening network ports (basic)

---

## 🧾 Script: `network_check.sh`

```bash
#!/bin/bash
# ---------------------------------------------
# Network Configuration Check Script
# Author: Sharad Patel
# Description: Performs basic Linux networking checks
# ---------------------------------------------

echo "========================================="
echo " Linux Network Configuration Check"
echo "========================================="
echo

section() {
    echo
    echo "---- $1 ----"
}

section "Hostname"
hostnamectl

section "Network Interfaces (ip link)"
ip -br link show

section "IP Address Configuration"
ip -br addr show

section "NetworkManager Status"
if systemctl is-active NetworkManager &>/dev/null; then
    echo "NetworkManager is running"
    nmcli device status
else
    echo "NetworkManager is NOT running"
fi

section "Routing Table"
ip route show

DEFAULT_GW=$(ip route | awk '/default/ {print $3}')
if [[ -n "$DEFAULT_GW" ]]; then
    echo "Default Gateway: $DEFAULT_GW"
else
    echo "No default gateway configured"
fi

section "DNS Configuration"
if [[ -f /etc/resolv.conf ]]; then
    cat /etc/resolv.conf
else
    echo "/etc/resolv.conf not found"
fi

section "Connectivity Test"
echo "Pinging default gateway..."
ping -c 2 "$DEFAULT_GW" &>/dev/null && echo "Gateway reachable" || echo "Gateway NOT reachable"

echo "Pinging public DNS (8.8.8.8)..."
ping -c 2 8.8.8.8 &>/dev/null && echo "Internet connectivity OK" || echo "Internet connectivity FAILED"

section "DNS Resolution Test"
getent hosts google.com &>/dev/null && echo "DNS resolution working" || echo "DNS resolution failed"

section "Listening Network Ports"
ss -tulnp | head -20

echo
echo "========================================="
echo " Network Check Completed"
echo "========================================="
````

---

## ▶️ Usage

### 1️⃣ Make the script executable

```bash
chmod +x network_check.sh
```

### 2️⃣ Run the script

```bash
./network_check.sh
```

### 3️⃣ (Optional) Run with root privileges

```bash
sudo ./network_check.sh
```

---

## 🧪 Tested On

* RHEL 8 / RHEL 9
* CentOS Stream
* Rocky Linux
* Ubuntu 20.04+
* Fedora

---

## 📘 RHCSA Relevance

* Uses modern tools: `ip`, `nmcli`, `ss`
* Avoids deprecated commands (`ifconfig`, `netstat`)
* Suitable for troubleshooting tasks in RHCSA exam environments

---

## 📂 Repository Structure

```text
.
├── network_check.sh
└── README.md
```

---

## 🚀 Future Enhancements

* Log output to file
* CSV report generation
* Podman / container network checks
* Minimal RHCSA exam-only version

---

## 👤 Author

**Sharad Patel**
Linux System Administrator | RHCSA Aspirant

---

## 📜 License

This project is licensed under the MIT License.

```

---

### ✅ Next Suggestions
If you want, I can also:
- Create a **professional GitHub repo description**
- Add a **LICENSE file (MIT)**
- Provide a **minimal RHCSA exam version**
- Improve this for **resume / Fiverr profile**

Just say the word 👍
```

