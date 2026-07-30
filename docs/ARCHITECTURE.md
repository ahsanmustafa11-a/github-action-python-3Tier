# DevSecOps Architecture

This document explains the overall architecture of the project and the execution flow of the GitHub Actions DevSecOps pipeline.

---

# Solution Architecture

```text
                   +------------------------+
                   |     GitHub Repository  |
                   +-----------+------------+
                               |
                               |
                        Push / Pull Request
                               |
                               v
                 +----------------------------+
                 |     GitHub Actions CI      |
                 +----------------------------+
                               |
        -----------------------------------------------------
        |          |          |         |         |          |
        v          v          v         v         v          v
     Lint     GitLeaks      SAST      SCA    SonarQube   Docker Build
                                                        + Hadolint
                                                              |
                                                              v
                                                      Trivy Image Scan
                                                              |
                                                              v
                                                     Docker Hub Registry
                                                              |
                                                              v
                                                Self Hosted GitHub Runner
                                                              |
                                                              v
                                                      AWS EC2 Deployment
                                                              |
                                                              v
                                                     OWASP ZAP DAST Scan
```

---

# AWS Infrastructure

```text
                    Internet
                        |
                        |
                 Public Elastic IP
                        |
                 +--------------+
                 | AWS EC2      |
                 | Ubuntu 26.04 |
                 +--------------+
                        |
        -----------------------------------
        |                 |               |
        v                 v               v
   SonarQube       GitHub Runner      Docker Engine
                                        |
                    ----------------------------------------
                    |               |                     |
                    v               v                     v
                Frontend        Backend             Nginx Reverse Proxy
```

---

# GitHub Actions Workflow

The project uses **Reusable Workflows** (`workflow_call`) to separate each stage of the DevSecOps pipeline into individual files.

| Workflow | Purpose |
|----------|---------|
| lint.yml | Python & JavaScript code quality |
| gitleaks.yml | Detect hardcoded secrets |
| sast.yml | Static Application Security Testing |
| sca.yml | Dependency vulnerability scanning |
| sonarqube.yml | Code quality and Quality Gate |
| docker-Hadolint-Login-push.yml | Dockerfile linting, build and push |
| trivy-image.yml | Docker image vulnerability scanning |
| deploy.yml | Deploy application to AWS EC2 |
| dast.yml | Dynamic Application Security Testing |

---

# DevSecOps Execution Flow

```text
Developer
     │
     ▼
Git Push
     │
     ▼
GitHub Actions
     │
     ▼
Code Linting
     │
     ▼
GitLeaks
     │
     ▼
SAST
     │
     ▼
SCA
     │
     ▼
SonarQube
     │
     ▼
Docker Build
     │
     ▼
Hadolint
     │
     ▼
Docker Push
     │
     ▼
Trivy Image Scan
     │
     ▼
Deploy to AWS EC2
     │
     ▼
OWASP ZAP DAST
```

---

# Project Components

## Backend

- Python
- Flask
- REST API

---

## Frontend

- HTML
- CSS
- JavaScript

---

## Database

- MySQL

---

## Containerization

- Docker
- Docker Compose

---

## CI/CD

- GitHub Actions
- Reusable Workflows
- Matrix Strategy

---

## Security

- Flake8
- ESLint
- GitLeaks
- Bandit
- Semgrep
- npm audit
- Hadolint
- Trivy
- SonarQube
- OWASP ZAP

---

# Deployment Flow

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
Application Live
```

---

# Repository Structure

```text
.
├── backend/
├── frontend/
├── database/
├── nginx/
├── docker-compose.yml
└── .github/
    └── workflows/
        ├── devsecops.yml
        ├── lint.yml
        ├── gitleaks.yml
        ├── sast.yml
        ├── sca.yml
        ├── sonarqube.yml
        ├── docker-Hadolint-Login-push.yml
        ├── trivy-image.yml
        ├── deploy.yml
        └── dast.yml
```

---

# Design Principles

- Modular GitHub Actions using `workflow_call`
- Reusable CI/CD workflows
- Shift-Left Security
- Infrastructure as Code mindset
- Automated Security Scanning
- Continuous Integration
- Continuous Deployment
- Defense in Depth
- Secure Container Lifecycle
