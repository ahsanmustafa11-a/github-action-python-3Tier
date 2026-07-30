# Security Guide

This project follows a **Shift-Left DevSecOps** approach by integrating multiple security tools throughout the CI/CD pipeline.

Instead of relying on a single scanner, each tool focuses on a different security layer, providing comprehensive coverage from source code to the deployed application.

---

# DevSecOps Security Pipeline

```text
Developer
     │
     ▼
Git Push
     │
     ▼
Lint
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
Hadolint
     │
     ▼
Docker Build
     │
     ▼
Trivy Image Scan
     │
     ▼
Deploy
     │
     ▼
OWASP ZAP
```

---

# Security Layers

| Layer | Tool |
|--------|------|
| Code Quality | Flake8, ESLint |
| Secret Detection | GitLeaks |
| Static Application Security Testing (SAST) | Bandit, Semgrep |
| Software Composition Analysis (SCA) | npm audit |
| Code Quality Analysis | SonarQube |
| Dockerfile Security | Hadolint |
| Container Image Security | Trivy |
| Dynamic Application Security Testing (DAST) | OWASP ZAP |

---

# Security Tools

---

## 1. Flake8

### Purpose

Checks Python code quality and coding standards.

### Detects

- Syntax Errors
- Unused Imports
- Undefined Variables
- PEP8 Violations
- Code Style Issues

### Stage

CI

Official Documentation

https://flake8.pycqa.org/

---

## 2. ESLint

### Purpose

Checks JavaScript code quality.

### Detects

- Syntax Errors
- Undefined Variables
- Unused Variables
- Bad Coding Practices
- Code Formatting Issues

### Stage

CI

Official Documentation

https://eslint.org/

---

## 3. GitLeaks

### Purpose

Prevents developers from accidentally committing secrets into Git.

### Detects

- AWS Keys
- Azure Keys
- GitHub Tokens
- DockerHub Tokens
- Passwords
- API Keys
- JWT Tokens
- Private Keys

### Stage

CI

Official Documentation

https://github.com/gitleaks/gitleaks

---

## 4. Bandit

### Purpose

Static security scanner for Python applications.

### Detects

- eval()
- exec()
- subprocess
- shell=True
- weak hashing
- insecure random
- unsafe yaml.load()
- insecure pickle
- hardcoded passwords

### Stage

SAST

Official Documentation

https://bandit.readthedocs.io/

---

## 5. Semgrep

### Purpose

Language-aware security scanner.

### Detects

- SQL Injection
- XSS
- SSRF
- Command Injection
- Path Traversal
- Hardcoded Secrets
- Insecure APIs
- Authentication Issues

### Stage

SAST

Official Documentation

https://semgrep.dev/docs

---

## 6. npm audit

### Purpose

Scans third-party JavaScript packages.

### Detects

- Vulnerable npm packages
- Known CVEs
- Dependency vulnerabilities

### Stage

SCA

Official Documentation

https://docs.npmjs.com/cli/v11/commands/npm-audit

---

## 7. SonarQube

### Purpose

Analyzes code quality, maintainability and security.

### Detects

- Bugs
- Vulnerabilities
- Code Smells
- Duplicated Code
- Security Hotspots
- Technical Debt

### Stage

CI

Official Documentation

https://docs.sonarsource.com/sonarqube-server/

---

## 8. Hadolint

### Purpose

Checks Dockerfiles against Docker best practices.

### Detects

- Latest tag usage
- Root user
- Missing HEALTHCHECK
- Unpinned packages
- Dockerfile best practice violations

### Stage

Container Security

Official Documentation

https://github.com/hadolint/hadolint

---

## 9. Trivy

### Purpose

Scans Docker images for vulnerabilities.

### Detects

- Operating System CVEs
- Python package vulnerabilities
- Node.js package vulnerabilities
- High & Critical CVEs
- Misconfigurations
- Secrets (optional)

### Stage

Container Security

Official Documentation

https://trivy.dev/latest/docs/

---

## 10. OWASP ZAP

### Purpose

Dynamic Application Security Testing (DAST).

Scans the running application after deployment.

### Detects

- SQL Injection
- XSS
- Missing Security Headers
- Cookie Issues
- Information Disclosure
- Authentication Weaknesses
- Directory Listing
- Server Misconfiguration

### Stage

DAST

Official Documentation

https://www.zaproxy.org/docs/

---

# Why Multiple Security Tools?

No single security tool can detect every type of issue.

Each tool specializes in a different area of the software development lifecycle.

| Tool | Focus Area |
|------|------------|
| Flake8 | Python Code Quality |
| ESLint | JavaScript Code Quality |
| GitLeaks | Secret Detection |
| Bandit | Python Security |
| Semgrep | Multi-language Security |
| npm audit | Dependency Security |
| SonarQube | Code Quality & Security |
| Hadolint | Dockerfile Security |
| Trivy | Container Image Security |
| OWASP ZAP | Runtime Security |

---

# Security Coverage

| Phase | Tool |
|---------|------|
| Source Code | Flake8, ESLint |
| Git Repository | GitLeaks |
| Static Analysis | Bandit, Semgrep |
| Dependencies | npm audit |
| Code Quality | SonarQube |
| Dockerfile | Hadolint |
| Docker Image | Trivy |
| Running Application | OWASP ZAP |

---

# Security Workflow

```text
Developer
      │
      ▼
Write Code
      │
      ▼
Lint
      │
      ▼
GitLeaks
      │
      ▼
Bandit
      │
      ▼
Semgrep
      │
      ▼
npm audit
      │
      ▼
SonarQube
      │
      ▼
Hadolint
      │
      ▼
Docker Build
      │
      ▼
Trivy
      │
      ▼
Deploy
      │
      ▼
OWASP ZAP
```

---

# Best Practices

- Never store secrets in source code.
- Keep dependencies updated.
- Review all security findings before deployment.
- Fail the pipeline on High and Critical vulnerabilities in production.
- Regularly update security scanning rules and tools.
- Monitor SonarQube Quality Gates before approving changes.
