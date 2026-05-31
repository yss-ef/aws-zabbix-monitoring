# AWS cloud monitoring infrastructure: centralized Zabbix deployment

Bottom Line Up Front: This project provides a robust, enterprise-grade
monitoring solution architected on Amazon Web Services (AWS). It implements a
centralized observability stack using Zabbix containerized via Docker to monitor
a hybrid cloud environment consisting of Linux and Windows Server EC2
instances.

## Technical architecture

The infrastructure is designed for high portability and visibility across a
distributed cloud network:

1.  **Monitoring core**: A Docker-composed stack (Zabbix Server, Web Frontend,
    and MySQL database) hosted on an AWS EC2 instance.
2.  **Telemetry collection**: Distributed Zabbix Agents deployed on target EC2
    instances (Ubuntu and Windows Server).
3.  **Network topology**: Deployed within a custom AWS VPC with granular
    security group rules for encrypted telemetry traffic.
4.  **Containerization**: Leveraging Docker for service isolation and rapid
    deployment of the monitoring core.

---

## Technical stack

*   **Cloud provider**: Amazon Web Services (AWS)
*   **Infrastructure**: EC2 (Elastic Compute Cloud), VPC (Virtual Private Cloud)
*   **Monitoring engine**: Zabbix 6.x / 7.x
*   **Containerization**: Docker / Docker Compose
*   **Operating systems**: Ubuntu (Linux), Windows Server 2022
*   **Database**: MySQL (Relational persistence for metrics)

---

## System features

### 1. Centralized observability
*   Single-pane-of-glass dashboard for monitoring disparate cloud assets.
*   Real-time health tracking of CPU, memory, disk I/O, and network throughput.
*   Automated alerting system for critical infrastructure events.

### 2. Containerized deployment
*   Microservices-based architecture for the Zabbix core.
*   Environment isolation using Docker volumes for persistent metric storage.
*   Simplified scaling and update cycles via Docker Compose orchestration.

### 3. Hybrid agent configuration
*   **Linux agents**: Automated installation and configuration via shell
    scripts for Ubuntu instances.
*   **Windows agents**: Systematic deployment for Windows Server monitoring
    using MSI installers and custom configuration files.
*   **Active/passive monitoring**: Support for both agent-push and server-pull
    data collection methods.

### 4. Cloud security
*   Ingress/egress filtering via AWS Security Groups (ports 10050/10051).
*   Encrypted communication between agents and the central server.
*   Role-based access control for the monitoring web interface.

---

## Project structure

```text
├── agents/          # Agent installation scripts (Linux/Windows)
├── architecture/    # Network diagrams and topology maps
├── report/          # Technical documentation and performance reports
├── zabbix-server/   # Docker orchestration files (.yml, .env)
└── README.md        # System documentation
```

---

## Deployment and setup

### Prerequisites
*   AWS account with EC2 permissions.
*   Docker and Docker Compose installed on the host instance.
*   Configured security groups for Zabbix communication.

### 1. Core server deployment
1.  Access your monitoring EC2 instance via SSH.
2.  Navigate to the server directory:
    ```bash
    cd zabbix-server
    ```
3.  Initialize the stack:
    ```bash
    docker-compose up -d
    ```

### 2. Agent provisioning
Refer to the `agents/` directory for platform-specific instructions to connect
remote instances to the central server.

---

## Access and governance

The monitoring interface is accessible via the EC2 Public IP on port 80.
*   **Default gateway**: `http://<EC2_PUBLIC_IP>`
*   **Authentication**: Admin / zabbix (Default - change upon initialization)

Authored by Youssef Fellah.
Developed for the Engineering Cycle - Mundiapolis University.
