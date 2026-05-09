# Cloud Architecture & Network Design

This directory thoroughly documents the cloud infrastructure deployed on Amazon Web Services (AWS) for the centralized monitoring project. It details the network topology, security configurations, and compute resource provisioning.

## Network Topology (VPC)

The infrastructure is built upon a single, unified Virtual Private Cloud (VPC) configured to securely host both the central monitoring server and the target agents.

### Technical Details

*   **VPC Name**: `Fellah-Youssef-VPC-Projet-Zabbix`
*   **CIDR Block**: `10.0.0.0/16`
*   **Subnet Type**: Public (configured to facilitate direct access and package downloads during provisioning).
*   **Availability Zone**: `us-east-1` (N. Virginia)

---

## Security (Security Groups)

Strict Security Groups have been implemented at the instance level to filter inbound network traffic, ensuring a secure communication channel between the agents and the central server while allowing administrative access.

### Allowed Traffic Matrix

| Protocol | Port | Source | Description |
| --- | --- | --- | --- |
| **TCP** | 80 / 443 | Web (Any) | Zabbix Web Interface (HTTP/HTTPS) |
| **TCP** | 10050 | VPC / Any | Zabbix Agent (Passive polling) |
| **TCP** | 10051 | VPC / Any | Zabbix Server / Traps (Active polling) |
| **TCP** | 22 | Admin IP | SSH Administration (Linux) |
| **TCP** | 3389 | Admin IP | RDP Administration (Windows) |

---

## Compute Resources (EC2)

The computing fleet consists of three specific instances, sized according to performance and budgetary requirements:

1.  **Zabbix Server** (`t2.medium`): Core instance hosting the Docker engine and the complete Zabbix stack (Server, Web GUI, Database).
2.  **Linux Client** (`t3.micro`): Target Ubuntu machine equipped with the Zabbix agent.
3.  **Windows Client** (`t3.medium`): Target Windows Server 2022 machine equipped with the Zabbix agent.

---

## Visual Documentation

*   [Architecture Diagram](security-schema.png)
*   [Infrastructure Screenshots](screenshots/)

Authored by Youssef Fellah.  
Developed for the Engineering Cycle - Mundiapolis University.
