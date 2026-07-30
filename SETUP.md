# Project Setup Guide

This guide explains how to configure the complete DevSecOps environment required to run this project.

---

# Prerequisites

Install the following software before running the project.

| Software | Version | Official Documentation |
|----------|---------|------------------------|
| Git | Latest | https://git-scm.com/downloads |
| Docker Engine | Latest | https://docs.docker.com/engine/install |
| Docker Compose | Latest | https://docs.docker.com/compose |
| Python | 3.11+ | https://www.python.org/downloads |
| Node.js | 20+ | https://nodejs.org |
| GitHub Actions | Cloud | https://docs.github.com/actions |
| Docker Hub Account | Required | https://hub.docker.com |
| AWS EC2 Ubuntu | 24.04/26.04 | https://aws.amazon.com/ec2 |
| SonarQube Community | Latest | https://docs.sonarsource.com/sonarqube-server |

---

# Clone Repository

```bash
git clone https://github.com/ahsanmustafa11-a/github-action-python-3Tier.git

cd github-action-python-3Tier
```

---

# GitHub Secrets

Repository

Settings

↓

Secrets and Variables

↓

Actions

Create the following secrets.

| Secret | Description |
|---------|-------------|
| DOCKERHUB_USERNAME | Docker Hub Username |
| DOCKERHUB_TOKEN | Docker Hub Personal Access Token |
| SONAR_HOST_URL | SonarQube Server URL |
| SONAR_TOKEN | SonarQube Project Token |
| HOST_IP | AWS EC2 Public IP |
| HOST_USERNAME | ubuntu |
| SSH_PRIVATE_KEY | EC2 Private Key (.pem contents) |

---

# Docker Hub

Create a Personal Access Token.

Official Guide

https://docs.docker.com/security/access-tokens/

---

# SonarQube

Create

- Project
- Token
- Quality Gate

Refer

https://docs.sonarsource.com/sonarqube-server

---

# AWS EC2

Recommended Configuration

| Resource | Recommended |
|----------|-------------|
| Instance | t3.large |
| vCPU | 2 |
| RAM | 8 GB |
| OS | Ubuntu 24.04 / 26.04 |
| Storage | 30 GB |

Open Ports

22

80

443

9000 (SonarQube)

---

# Self Hosted Runner

Configure the GitHub Self Hosted Runner on the deployment server.

Official Guide

https://docs.github.com/actions/hosting-your-own-runners

---

# How to Run the Project Locally

Start all containers.

```bash
docker compose up --build -d
```

Verify running containers.

```bash
docker ps
```

Stop containers.

```bash
docker compose down
```

View logs.

```bash
docker compose logs -f
```

Rebuild containers.

```bash
docker compose build --no-cache
```

Restart services.

```bash
docker compose restart
```

---

# Run Without Docker

Backend

```bash
cd backend

pip install -r requirements.txt

python app.py
```

Frontend

Serve the frontend using any web server such as Nginx or VS Code Live Server.

---

# Verify CI/CD

Push any commit to the main branch.

```bash
git add .

git commit -m "Test DevSecOps Pipeline"

git push origin main
```

The GitHub Actions pipeline will automatically execute:

- Code Linting
- GitLeaks
- SAST
- SCA
- Docker Build
- Trivy Scan
- SonarQube Analysis
- Deploy to AWS EC2
- OWASP ZAP DAST Scan

---

# Official Documentation

GitHub Actions

https://docs.github.com/actions

Docker

https://docs.docker.com

Docker Compose

https://docs.docker.com/compose

SonarQube

https://docs.sonarsource.com/sonarqube-server

Trivy

https://trivy.dev/latest/docs

OWASP ZAP

https://www.zaproxy.org/docs

GitLeaks

https://github.com/gitleaks/gitleaks

Semgrep

https://semgrep.dev/docs

Bandit

https://bandit.readthedocs.io

Hadolint

https://github.com/hadolint/hadolint
