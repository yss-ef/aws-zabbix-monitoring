# Zabbix Server Infrastructure (Docker)

This directory contains the complete Docker Compose configuration required to deploy a production-ready Zabbix monitoring stack. Containerization ensures environmental parity, rapid deployment, and isolated dependency management on AWS instances.

## Included Services

The stack is composed of three primary microservices working in orchestration:

*   **`zabbix-server`**: The central processing engine of the monitoring system.
*   **`zabbix-web`**: The graphical user interface (powered by Nginx).
*   **`zabbix-db`**: A MySQL 8.0 relational database for robust data persistence.

---

## Deployment Guide

Follow these steps to deploy the stack on an Ubuntu-based AWS EC2 instance.

1.  **Install Docker & Docker Compose**:
    Update your package list and install the container engine:
    ```bash
    sudo apt update && sudo apt install docker.io docker-compose -y
    ```

2.  **Launch the Stack**:
    Navigate to this directory and start the containers in detached (background) mode:
    ```bash
    docker-compose up -d
    ```

3.  **Verify Container Status**:
    Ensure all services are healthy and running:
    ```bash
    docker ps
    ```

---

## Configuration & Security

Environment variables are decoupled from the main compose file using dedicated `.env` files to protect sensitive credentials and simplify configuration.

*   **.env_db_mysql**: Database credentials and root passwords.
*   **.env_srv**: Backend server parameters (cache sizes, timeout, etc.).
*   **.env_web**: Frontend settings (PHP Timezone, Server display name).

---

## Accessing the Interface

Once the deployment is finalized, the Zabbix Web interface is accessible via the public IP of your AWS instance:

*   **URL**: `http://<AWS_PUBLIC_IP>:80`
*   **Default Credentials**:
    *   **Login**: `Admin`
    *   **Password**: `zabbix`

Authored by Youssef Fellah.  
Developed for the Engineering Cycle - Mundiapolis University.
