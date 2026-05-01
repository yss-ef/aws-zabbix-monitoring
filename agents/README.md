# Zabbix Monitoring Agents (Clients)

This directory contains the automation scripts and configuration files required to provision and connect target AWS EC2 instances (Linux and Windows) to the central Zabbix monitoring server.

## Overview

The scripts provided here automate the installation of the Zabbix Agent, configure the `zabbix_agentd.conf` file to point to the central server's IP address, and ensure the service is enabled to start on boot.

---

## Linux Client (Ubuntu)

### Deployment & Installation

1.  **Transfer the deployment script**:
    From your local terminal, use `scp` to push the installation script to your target Ubuntu instance:
    ```bash
    scp -i /path/to/your/aws-key.pem install_agent.sh ubuntu@<TARGET_EC2_PUBLIC_IP>:/home/ubuntu/
    ```

2.  **Execute the script**:
    SSH into the target machine, make the script executable, and run it with root privileges:
    ```bash
    ssh -i /path/to/your/aws-key.pem ubuntu@<TARGET_EC2_PUBLIC_IP>
    chmod +x install_agent.sh
    sudo ./install_agent.sh
    ```

3.  **Configuration Details**:
    The script will automatically prompt for the Zabbix Server IP and the Hostname of the current machine to inject them into `/etc/zabbix/zabbix_agentd.conf`.

---

## Windows Client (Windows Server)

### Deployment & Installation

1.  **Transfer configuration files**:
    Connect to the Windows Server EC2 instance via RDP. Transfer the provided Windows agent archive and configuration script.

2.  **Execution**:
    Open PowerShell as an Administrator and execute the deployment script:
    ```powershell
    Set-ExecutionPolicy Bypass -Scope Process -Force
    .\install_agent.ps1
    ```

3.  **Configuration Details**:
    The PowerShell script installs the Zabbix Agent as a Windows Service, opens the required firewall port (10050), and configures the `Server` and `Hostname` parameters in `C:\zabbix\zabbix_agentd.conf`.

---

## Troubleshooting

If the central server cannot reach an agent, verify the following:

*   **AWS Security Groups**: Ensure port 10050 (TCP) is open for inbound traffic from the Zabbix Server's IP.
*   **Service Status (Linux)**: `systemctl status zabbix-agent`
*   **Service Status (Windows)**: `Get-Service 'Zabbix Agent'`

---

*Authored by Youssef Fellah.*

*Developed for the Engineering Cycle - Mundiapolis University.*
