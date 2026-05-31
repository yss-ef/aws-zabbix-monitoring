# Cloud architecture and network design

Bottom Line Up Front: This directory documents the cloud infrastructure deployed
on Amazon Web Services (AWS) for the centralized monitoring project. It details
the network topology, security configurations, and compute resource
provisioning.

## Network topology (VPC)

The infrastructure is built upon a single, unified Virtual Private Cloud (VPC)
configured to securely host both the central monitoring server and the target
agents.

### Technical details

*   **VPC name**: `Fellah-Youssef-VPC-Projet-Zabbix`
*   **CIDR block**: `10.0.0.0/16`
*   **Subnet type**: Public (configured to facilitate direct access and package
    downloads during provisioning).
*   **Availability zone**: `us-east-1` (N. Virginia)

---

## Security (security groups)

Strict security groups have been implemented at the instance level to filter
inbound network traffic, ensuring a secure communication channel between the
agents and the central server while allowing administrative access.

### Allowed traffic matrix

| Protocol | Port | Source | Description |
| --- | --- | --- | --- |
| **TCP** | 80 / 443 | Web (Any) | Zabbix Web Interface (HTTP/HTTPS) |
| **TCP** | 10050 | VPC / Any | Zabbix Agent (Passive polling) |
| **TCP** | 10051 | VPC / Any | Zabbix Server / Traps (Active polling) |
| **TCP** | 22 | Admin IP | SSH Administration (Linux) |
| **TCP** | 3389 | Admin IP | RDP Administration (Windows) |

---

## Compute resources (EC2)

The computing fleet consists of three specific instances, sized according to
performance and budgetary requirements:

1.  **Zabbix server** (`t2.medium`): Core instance hosting the Docker engine
    and the complete Zabbix stack (Server, Web GUI, database).
2.  **Linux client** (`t3.micro`): Target Ubuntu machine equipped with the
    Zabbix agent.
3.  **Windows client** (`t3.medium`): Target Windows Server 2022 machine
    equipped with the Zabbix agent.

---

## Visual documentation

*   [Architecture diagram](security-schema.png)
*   [Infrastructure screenshots](screenshots/)

Authored by Youssef Fellah.
Developed for the Engineering Cycle - Mundiapolis University.
