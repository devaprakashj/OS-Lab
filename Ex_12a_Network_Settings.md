# Exercise 12 (a): Configure Basic Network Settings (IP, DNS, Gateway)

## 🎯 Aim
To configure basic network settings in Linux including IP Address, Subnet Mask, Default Gateway, and DNS Server.

## 📚 Theory
A computer network requires proper configuration to communicate with other systems. 

**Important network parameters:**
| Parameter | Description |
|:---:|---|
| **IP Address** | Unique address assigned to a device in the network |
| **Subnet Mask** | Defines network and host portions of an IP address |
| **Gateway** | Router used to communicate with other networks |
| **DNS** | Converts domain names into IP addresses |

Linux provides commands such as `ip`, `ifconfig`, `route`, and `nmcli` to configure network settings.

---

## 📝 Procedure

### Step 1: Check Network Interfaces
Open terminal and type:
```bash
ip addr
```
*This shows available interfaces such as `eth0`, `ens33`, or `wlan0`.*

### Step 2: Assign IP Address
Example (assuming interface is `ens33`):
```bash
sudo ip addr add 192.168.1.100/24 dev ens33
```
*Where:*
- `192.168.1.100` → IP Address
- `/24` → Subnet mask (`255.255.255.0`)

### Step 3: Bring Network Interface Up
```bash
sudo ip link set ens33 up
```

### Step 4: Configure Default Gateway
```bash
sudo ip route add default via 192.168.1.1
```

### Step 5: Configure DNS Server
Edit DNS configuration file:
```bash
sudo nano /etc/resolv.conf
```
Add the following lines to the file:
```text
nameserver 8.8.8.8
nameserver 8.8.4.4
```

### Step 6: Verify Network Configuration
Check IP:
```bash
ip addr
```
Check gateway:
```bash
ip route
```
Test connectivity:
```bash
ping google.com
```

---

## 💻 Implementation Code (Commands Summary)
```bash
ip addr
sudo ip addr add 192.168.1.100/24 dev ens33
sudo ip link set ens33 up
sudo ip route add default via 192.168.1.1
sudo nano /etc/resolv.conf
ping google.com
```

---

## 📥 Sample Input & Output

**Sample Configuration:**
- **IP Address:** `192.168.1.100`
- **Subnet Mask:** `255.255.255.0`
- **Gateway:** `192.168.1.1`
- **DNS Server:** `8.8.8.8`

**Sample Output of `ip addr`:**
```text
2: ens33: <BROADCAST,MULTICAST,UP,LOWER_UP>
    inet 192.168.1.100/24 brd 192.168.1.255 scope global ens33
```

**Sample Output of `ping`:**
```text
PING google.com (142.250.182.14): 56 data bytes
64 bytes from 142.250.182.14: icmp_seq=1 ttl=117 time=20 ms
```

---

## ✅ Result
Basic network settings including IP address, gateway, and DNS were successfully configured and verified.
