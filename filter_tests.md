# Network Traffic Filtering Test Results

## Overview
This document contains test execution logs validating network access control policies configured on `imani-Virtual-Machine` (192.168.10.100) enforced via `iptables` rules.

---

## Test Environment Setup
- **Server VM:** `imani-Virtual-Machine` (Target Web Server on Port 80)
  - IP Address: `192.168.10.100/24`
- **Client VM:** `faith-Virtual-Machine`
  - Staff Interface Alias: `192.168.10.15/24`
  - Guest Interface Alias: `192.168.20.45/24`

---

## Applied Firewall Policy (`iptables`)
```bash
sudo iptables -F
sudo iptables -P INPUT DROP
sudo iptables -P FORWARD DROP
sudo iptables -A INPUT -i lo -j ACCEPT
sudo iptables -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT
sudo iptables -A INPUT -s 192.168.20.0/24 -j DROP
sudo iptables -A INPUT -s 192.168.10.0/24 -p tcp --dport 80 -j ACCEPT
sudo iptables -A INPUT -p tcp --dport 80 -j DROP

---

## Empirical Test Execution Log

### Test 1: Permitted Access — Staff Subnet on Port 80 (HTTP)
* **Command Executed:** 
  ```bash
  nc -zv -s 192.168.10.15 192.168.10.100 80
