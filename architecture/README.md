# 🏗️ Cloud Architecture & Network Design

> **Infrastructure Submodule**
> This directory thoroughly documents the cloud infrastructure deployed on **Amazon Web Services (AWS)** for the centralized monitoring project. It details the network topology, security configurations, and compute resource provisioning.

## 📑 Table of Contents

* [Network Topology (VPC)](https://www.google.com/search?q=%23%EF%B8%8F-network-topology-vpc)
* [Security (Security Groups)](https://www.google.com/search?q=%23%EF%B8%8F-security-security-groups)
* [Compute Resources (EC2)](https://www.google.com/search?q=%23-compute-resources-ec2)

## 🗺️ Network Topology (VPC)

The infrastructure is built upon a single, unified **Virtual Private Cloud (VPC)** configured to securely host both the central monitoring server and the target agents.

### Technical Details

* **VPC Name:** `Fellah-Youssef-VPC-Projet-Zabbix`
* **CIDR Block:** `10.0.0.0/16`
* **Subnet Type:** Public (configured to facilitate direct access and package downloads during provisioning).
* **Availability Zone:** `us-east-1` (N. Virginia)

## 🛡️ Security (Security Groups)

Strict Security Groups have been implemented at the instance level to filter inbound network traffic, ensuring a secure communication channel between the agents and the central server while allowing administrative access.

### Allowed Traffic Matrix

| Protocol | Port | Source | Description |
| --- | --- | --- | --- |
| **TCP** | `80` / `443` | Web (Any) | Zabbix Web Interface (HTTP/HTTPS) |
| **TCP** | `10050` | VPC / Any | Zabbix Agent (Passive polling) |
| **TCP** | `10051` | VPC / Any | Zabbix Server / Traps (Active polling) |
| **TCP** | `22` | Admin IP | SSH Administration (Linux) |
| **TCP** | `3389` | Admin IP | RDP Administration (Windows) |

## 💻 Compute Resources (EC2)

The computing fleet consists of 3 specific instances, meticulously sized according to the project's performance and budgetary recommendations.

1. **Zabbix Server** (`t2.medium`): The core instance hosting the Docker engine and the complete Zabbix stack (Server, Web GUI, Database).
2. **Linux Client** (`t3.micro`): The target Ubuntu machine equipped with the Zabbix agent.
3. **Windows Client** (`t3.medium`): The target Windows Server 2022 machine equipped with the Zabbix agent.

---

*Authored by Youssef Fellah.*

*Developed as part of the 2nd year Engineering Cycle - Mundiapolis University.*
