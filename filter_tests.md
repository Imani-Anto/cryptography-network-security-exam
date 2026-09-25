# Network Traffic Filtering Configuration & Execution Log

## 1. Test Environment Setup
* **Server VM:** `imani-Virtual-Machine` (Target Web Server on Port 80)
  * **IP Address:** `192.168.10.100/24`
* **Client VM:** `faith-Virtual-Machine`
  * **Staff Interface Alias:** `192.168.10.15/24`
  * **Guest Interface Alias:** `192.168.20.45/24`

---

## 2. Applied Firewall Policy (iptables)

```bash
# Flush existing rules and set default-deny policy
sudo iptables -F
sudo iptables -P INPUT DROP
sudo iptables -P FORWARD DROP

# Allow loopback and established connections
sudo iptables -A INPUT -i lo -j ACCEPT
sudo iptables -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT

# Explicitly drop all ingress traffic from Guest network
sudo iptables -A INPUT -s 192.168.20.0/24 -j DROP

# Permit HTTP access specifically for Staff network
sudo iptables -A INPUT -s 192.168.10.0/24 -p tcp --dport 80 -j ACCEPT

# Drop all remaining port 80 traffic
sudo iptables -A INPUT -p tcp --dport 80 -j DROP