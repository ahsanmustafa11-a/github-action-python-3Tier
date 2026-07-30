# 🚀 GitHub Actions DevSecOps CI/CD Pipeline

A complete **DevSecOps CI/CD pipeline** built using **GitHub Actions** for a Python 3-Tier application.

This project demonstrates how to implement modern DevSecOps practices by integrating code quality, security scanning, container security, continuous deployment, and dynamic application security testing into a reusable GitHub Actions workflow.

---

# 📌 Features

- Reusable GitHub Actions Workflows
- Matrix Strategy
- Python Backend Linting (Flake8)
- JavaScript Frontend Linting (ESLint)
- GitLeaks Secret Detection
- Bandit Security Scan
- Semgrep SAST
- npm audit Dependency Scan
- Hadolint Dockerfile Linting
- Docker Image Build
- DockerHub Push
- Trivy Container Image Scan
- SonarQube Code Analysis
- Self Hosted GitHub Runner
- Continuous Deployment (CD)
- OWASP ZAP DAST Scan

---

# 🛠 Tech Stack

| Category | Technology |
|----------|------------|
| CI/CD | GitHub Actions |
| Backend | Python, Flask |
| Frontend | HTML, CSS, JavaScript |
| Database | MySQL |
| Reverse Proxy | Nginx |
| Containers | Docker |
| Registry | Docker Hub |
| Code Quality | Flake8, ESLint |
| Secret Scanning | GitLeaks |
| SAST | Bandit, Semgrep |
| SCA | npm audit |
| Docker Security | Hadolint, Trivy |
| Code Analysis | SonarQube Community |
| DAST | OWASP ZAP |
| Deployment | AWS EC2 + Self Hosted Runner |

---

# 📂 Repository Structure

```text
.github/
└── workflows/
    ├── devsecops.yml
    ├── lint.yml
    ├── frontend-lint.yml
    ├── gitleaks.yml
    ├── sast.yml
    ├── sca.yml
    ├── docker-Hadolint-Login-push.yml
    ├── docker-build-scan-push.yml
    ├── trivy-image.yml
    ├── sonarqube.yml
    ├── deploy.yml
    └── dast.yml

backend/
frontend/
database/
nginx/
```

---

# 🔄 DevSecOps Pipeline

```
Developer
     │
     ▼
GitHub Push
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
Dockerfile Lint
     │
     ▼
Docker Build
     │
     ▼
Trivy Scan
     │
     ▼
SonarQube Analysis
     │
     ▼
DockerHub
     │
     ▼
Deploy to AWS EC2
     │
     ▼
OWASP ZAP DAST
```

---

# 📖 Documentation

Additional documentation is available in this repository.

| File | Description |
|------|-------------|
| SETUP.md | Installation and configuration guide |
| ARCHITECTURE.md | Pipeline architecture |
| SECURITY.md | Security tools overview |
| SONARQUBE.md | SonarQube setup |
| DEPLOYMENT.md | Deployment using Self Hosted Runner |
| TROUBLESHOOTING.md | Common issues and fixes |

---

# 🔐 Security Tools

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

# 📸 Screenshots

Add screenshots for:

- GitHub Actions Pipeline
- SonarQube Dashboard
- DockerHub Images
- Trivy Scan Report
- OWASP ZAP Report
- AWS Deployment

---

# 📚 Official Documentation

- GitHub Actions: https://docs.github.com/actions
- Docker: https://docs.docker.com
- SonarQube: https://docs.sonarsource.com/sonarqube-server
- Trivy: https://trivy.dev/latest/docs
- OWASP ZAP: https://www.zaproxy.org/docs

---

# 📄 License

This project is licensed under the MIT License.
