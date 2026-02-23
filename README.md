# ☁️ AWS Centralized Cloud Monitoring Infrastructure | Zabbix & Docker

> **Academic Project - Cloud Computing** | **Year:** 2025/2026 | **Author:** Youssef Fellah

## 📑 Table of Contents

* [Project Overview](https://www.google.com/search?q=%23-project-overview)
* [Video Presentation](https://www.google.com/search?q=%23-video-presentation)
* [Architecture](https://www.google.com/search?q=%23%EF%B8%8F-architecture)
* [Repository Structure](https://www.google.com/search?q=%23-repository-structure)
* [Quick Start Guide](https://www.google.com/search?q=%23-quick-start-guide)
* [Web Interface Access](https://www.google.com/search?q=%23-web-interface-access)
* [Project Report](https://www.google.com/search?q=%23-project-report)

## 📋 Project Overview

This project focuses on implementing a **centralized monitoring infrastructure** hosted on **Amazon Web Services (AWS)**. The goal is to deploy a robust solution capable of providing real-time monitoring for a hybrid IT environment consisting of **Linux (Ubuntu)** and **Windows Server** instances.

The technical solution relies on containerizing the **Zabbix** server using **Docker**, which guarantees high portability, strict isolation, and simplified deployment procedures.

## 📽️ Video Presentation

Click the image below to watch the full project demonstration on YouTube:

## 🏗️ Architecture

The infrastructure is deployed within an AWS VPC using the following topology:

* **Network:** Single VPC with a public subnet and strict Security Groups mapping.
* **Server:** An EC2 `t2.medium` instance hosting the Docker stack (Zabbix Server + Web Interface + Database).
* **Agents:** EC2 instances (Linux `t3.micro` & Windows `t3.medium`) configured with active Zabbix agents.

📂 **[View architecture details and network diagrams](https://www.google.com/search?q=./architecture/README.md)**

## 📂 Repository Structure

```text
.
├── 📂 agents/           # Installation scripts and client configurations (Linux/Windows)
├── 📂 architecture/     # Network diagrams and configuration proofs (Screenshots)
├── 📂 rapport/          # Final deliverable (PDF) and source files
├── 📂 server-zabbix/    # Docker deployment files (docker-compose.yml, .env)
└── README.md            # This file

```

## 🚀 Quick Start Guide

### 1. Prerequisites

* An active AWS account.
* An SSH key pair (`.pem`) for instance access.
* **Local Machine Preparation (Fedora 43):**
Ensure you have the necessary tools to connect to your AWS infrastructure and manage the repository:
```bash
sudo dnf install openssh-clients git docker

```



### 2. Server Installation

Connect to your AWS server instance via SSH, then clone this repository:

```bash
git clone https://github.com/yss-ef/[YOUR_REPO_NAME].git
cd [YOUR_REPO_NAME]/server-zabbix

```

Launch the stack using Docker Compose:

```bash
sudo docker-compose up -d

```

### 3. Agent Installation

To connect your client machines (Ubuntu/Windows) to the central server, follow the detailed instructions in the dedicated folder:
👉 **[Consult the Agent Installation Guide](https://www.google.com/search?q=./agents/README.md)**

## 🌐 Web Interface Access

Once the Docker deployment is complete and the containers are healthy, the Zabbix Web interface is accessible via the public IP address of your AWS instance:

* **URL:** `http://<YOUR_PUBLIC_IP>:80`
* **Default Login:** `Admin`
* **Default Password:** `zabbix`

## 📄 Project Report

The comprehensive technical report, including architectural justifications and operational proofs, is available here:

📥 **[Download the PDF Report](https://www.google.com/search?q=./rapport/Examen_Cloud_Fellah_Youssef.pdf)**

---

*Developed as part of the 2nd year Engineering Cycle - Mundiapolis University.*
