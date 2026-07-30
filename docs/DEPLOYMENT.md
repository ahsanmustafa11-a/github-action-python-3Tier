# Deployment Guide

This project uses **GitHub Actions** with a **Self-Hosted Runner** to automatically deploy the application to an AWS EC2 instance after all CI and security checks pass.

---

# Deployment Architecture

```text
Developer
      │
      ▼
GitHub Repository
      │
      ▼
GitHub Actions
      │
      ▼
Docker Hub
      │
      ▼
Self Hosted Runner
      │
      ▼
AWS EC2
      │
      ▼
Docker Compose
      │
      ▼
Frontend + Backend + Database + Nginx
```

---

# Deployment Prerequisites

Before enabling deployment, ensure you have:

- AWS EC2 Ubuntu Server
- Docker Engine
- Docker Compose
- Git
- GitHub Self Hosted Runner
- Docker Hub Account

Official Documentation

GitHub Self Hosted Runner

https://docs.github.com/actions/hosting-your-own-runners

Docker

https://docs.docker.com/

Docker Compose

https://docs.docker.com/compose/

---

# AWS EC2 Recommendation

| Resource | Recommended |
|----------|-------------|
| Instance | t3.large |
| OS | Ubuntu 24.04 / 26.04 |
| CPU | 2 vCPU |
| RAM | 8 GB |
| Storage | 30 GB |

---

# Required GitHub Secrets

Navigate to

Repository

↓

Settings

↓

Secrets and Variables

↓

Actions

Create the following Secrets.

| Secret | Description |
|----------|-------------|
| HOST_IP | EC2 Public IP |
| HOST_USERNAME | ubuntu |
| SSH_PRIVATE_KEY | Private SSH Key (.pem contents) |
| DOCKERHUB_USERNAME | Docker Hub Username |
| DOCKERHUB_TOKEN | Docker Hub Personal Access Token |

---

# Self Hosted Runner

Install a GitHub Self Hosted Runner on the deployment server.

Official Documentation

https://docs.github.com/actions/hosting-your-own-runners

Recommended Runner Labels

```text
self-hosted
linux
ubuntu
production
```

Use the same label in your deployment workflow.

Example

```yaml
runs-on:
  - self-hosted
  - linux
```

---

# Docker Compose

The deployment workflow pulls the latest Docker images from Docker Hub and starts the application using Docker Compose.

Common commands:

Start application

```bash
docker compose up -d
```

Pull latest images

```bash
docker compose pull
```

Restart services

```bash
docker compose restart
```

Stop services

```bash
docker compose down
```

View running containers

```bash
docker ps
```

View logs

```bash
docker compose logs -f
```

---

# Deployment Workflow

Deployment starts automatically after:

- Lint
- GitLeaks
- SAST
- SCA
- SonarQube
- Docker Build
- Trivy Scan

Pipeline

```text
CI Completed
      │
      ▼
GitHub Actions
      │
      ▼
Self Hosted Runner
      │
      ▼
docker compose pull
      │
      ▼
docker compose up -d
      │
      ▼
Application Live
```

---

# Verify Deployment

After deployment, verify:

- GitHub Actions job completed successfully.
- Self Hosted Runner is online.
- Docker containers are running.
- Application is accessible via the EC2 Public IP.
- Nginx is serving the application correctly.

Useful commands:

```bash
docker ps
```

```bash
docker images
```

```bash
docker compose ps
```

```bash
docker compose logs -f
```

---

# Updating the Application

After making code changes:

```bash
git add .

git commit -m "Update application"

git push origin main
```

GitHub Actions will automatically:

- Build the application
- Run security scans
- Push Docker images
- Deploy the latest version to AWS EC2

---

# Rollback

If deployment fails, redeploy the previous stable Docker image by updating the image tag in your `docker-compose.yml` and restarting the services.

Example:

```bash
docker compose down

docker compose pull

docker compose up -d
```

---

# Common Issues

## Runner Offline

Check the runner service.

```bash
sudo ./svc.sh status
```

---

## Docker Login Failed

Verify:

- DOCKERHUB_USERNAME
- DOCKERHUB_TOKEN

GitHub Secrets are configured correctly.

---

## Image Not Found

Ensure:

- Docker image was pushed successfully.
- Image tag matches `docker-compose.yml`.

---

## Deployment Failed

Verify:

- Docker service is running.
- Docker Compose file is valid.
- Runner has network access.
- Disk space is available.

---

# Official Documentation

GitHub Actions

https://docs.github.com/actions

GitHub Self Hosted Runner

https://docs.github.com/actions/hosting-your-own-runners

Docker

https://docs.docker.com/

Docker Compose

https://docs.docker.com/compose/

AWS EC2

https://docs.aws.amazon.com/ec2/
