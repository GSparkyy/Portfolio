# Ubuntu Server Setup and Hardening on VirtualBox

## Environment
- **VirtualBox version**: `7.1.190169112-win`
- **Server ISO**: `ubuntu-24.04.2-live-server`
- **Kali VM used for scanning and remote access**

---

## Initial Setup

```bash
sudo apt update && sudo apt upgrade -y
```
_Updates and upgrades all available packages after installing the server._

---

## Baseline Scan (Kali VM)

```bash
nmap -A <SERVER_IP> -oN baseline_scan_UbuntuLab.txt
```
![Screenshot 2025-07-07 124202](https://github.com/user-attachments/assets/c9ce1a65-70e8-4118-8c90-54118729b467)

_Performs an aggressive scan on the fresh server and saves results to a text file._  
⚠️ _No firewall protection at this stage._

---

## Basic Server Hardening

### Enable SSH Access Before Firewall

```bash
sudo ufw allow OpenSSH
```

### Enable UFW Firewall

```bash
sudo ufw enable
```
_Activates uncomplicated firewall with default settings._

### Review Active Services

```bash
sudo systemctl list-units --type=service
```
_Checks for unneeded or vulnerable services running. (I found none)_

### Install Fail2Ban

```bash
sudo apt install fail2ban -y
sudo fail2ban-client status sshd
```
_Adds brute force protection._

### Enable UFW Logging

```bash
sudo ufw logging low
```
_Logs blocked access attempts._

---

## SSH Key Authentication

### Generate RSA Key Pair

```bash
ssh-keygen
```

### Configure SSH Server

```bash
sudo nano /etc/ssh/sshd_config
```
_Add or edit the line to disable password authentication:_

```text
#PasswordAuthentication no
```

### Restart SSH Service

```bash
sudo systemctl restart ssh
```

---

## Enable Automatic Updates

```bash
sudo apt install unattended-upgrades
sudo dpkg-reconfigure unattended-upgrades
```

---

## Reboot the Server

```bash
sudo reboot
```

---

## Monitor UFW Logs

```bash
sudo tail -f /var/log/ufw.log
```
_Live updates of firewall activity._

---

## Hardened Scan (Kali VM)

```bash
nmap -A <SERVER_IP> -oN hardened_scan_UbuntuLab.txt
```
![Screenshot 2025-07-07 131949](https://github.com/user-attachments/assets/64e34ad8-891b-469c-b847-c6464ed6aa4f)

_Scans the hardened server for comparison._

---

## Remote SSH Access (Kali VM)

```bash
ssh gsparkyy@<SERVER_IP>
```
![Screenshot 2025-07-07 132441](https://github.com/user-attachments/assets/a16c2e62-c058-4610-9c96-945bb5605f85)

_Remote connection to the server._

---
