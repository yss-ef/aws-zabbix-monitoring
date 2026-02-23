# 🕵️ Zabbix Monitoring Agents (Clients)

> **Infrastructure Provisioning Submodule**
> This directory contains the automation scripts and configuration files required to provision and connect your target AWS EC2 instances (Linux and Windows) to the central Zabbix monitoring server.

## 📑 Table of Contents

* [Overview](https://www.google.com/search?q=%23-overview)
* [Linux Client (Ubuntu)](https://www.google.com/search?q=%23-linux-client-ubuntu)
* [Windows Client (Windows Server)](https://www.google.com/search?q=%23-windows-client-windows-server)
* [Troubleshooting](https://www.google.com/search?q=%23%EF%B8%8F-troubleshooting)

## 📋 Overview

The scripts provided here automate the installation of the Zabbix Agent, configure the `zabbix_agentd.conf` file to point to your central server's IP address, and ensure the service is enabled to start on boot.

## 🐧 Linux Client (Ubuntu)

### Deployment & Installation

**1. Transfer the deployment script**
From your local **Fedora 43** terminal, use `scp` to push the installation script to your target Ubuntu instance on AWS:

```bash
scp -i /path/to/your/aws-key.pem install_agent.sh ubuntu@<TARGET_EC2_PUBLIC_IP>:/home/ubuntu/

```

**2. Execute the script on the target instance**
SSH into the target machine, make the script executable, and run it with root privileges:

```bash
ssh -i /path/to/your/aws-key.pem ubuntu@<TARGET_EC2_PUBLIC_IP>
chmod +x install_agent.sh
sudo ./install_agent.sh

```

**3. Configuration Details**
The script will automatically prompt you for the **Zabbix Server IP** and the **Hostname** of the current machine to inject them into `/etc/zabbix/zabbix_agentd.conf`.

## 🪟 Windows Client (Windows Server)

### Deployment & Installation

**1. Transfer the configuration files**
Connect to your Windows Server EC2 instance via RDP. Transfer the provided Windows agent archive and configuration script.

**2. Execution**
Open PowerShell as an Administrator and execute the deployment script:

```powershell
Set-ExecutionPolicy Bypass -Scope Process -Force
.\install_agent.ps1

```

**3. Configuration Details**
The PowerShell script will install the Zabbix Agent as a Windows Service, open the required firewall port (10050), and configure the `Server` and `Hostname` parameters in the configuration file located at `C:\zabbix\zabbix_agentd.conf`.

## 🛠️ Troubleshooting

If the central server cannot reach an agent, verify the following:

* **AWS Security Groups:** Ensure port `10050` (TCP) is open for inbound traffic from the Zabbix Server's IP.
* **Service Status (Linux):** `systemctl status zabbix-agent`
* **Service Status (Windows):** `Get-Service 'Zabbix Agent'`

---

*Authored by Youssef Fellah.*

*Developed as part of the 2nd year Engineering Cycle - Mundiapolis University.*
