# SonarQube Setup

This project uses **SonarQube Community Edition** to analyze source code for bugs, vulnerabilities, code smells, duplicated code, and maintainability issues before deployment.

---

# Prerequisites

Before configuring SonarQube, ensure you have:

- SonarQube Community Edition
- Java 17 or later
- AWS EC2 (Recommended: t3.large or higher)
- GitHub Repository
- GitHub Actions

Official Documentation

https://docs.sonarsource.com/sonarqube-server/

---

# Recommended AWS Configuration

| Resource | Recommendation |
|-----------|----------------|
| Instance Type | t3.large |
| vCPU | 2 |
| Memory | 8 GB |
| Storage | 30 GB |
| Operating System | Ubuntu 24.04 / 26.04 |

> **Note:** Running SonarQube on a `t3.small` (2 GB RAM) is not recommended and may cause the service to crash due to insufficient memory.

---

# Configure SonarQube

## Step 1 - Create a Project

1. Log in to SonarQube.
2. Click **Create Project**.
3. Select **Manually**.
4. Enter a project name.
5. Generate a project token.

Save the generated token securely.

---

## Step 2 - Generate a Token

Navigate to:

```
Administration
    ↓
Security
    ↓
Users
    ↓
Tokens
```

Create a new token and copy it.

---

# GitHub Repository Secrets

Go to:

```
Repository
    ↓
Settings
    ↓
Secrets and Variables
    ↓
Actions
```

Add the following secrets.

| Secret | Example |
|----------|----------|
| SONAR_HOST_URL | http://YOUR_PUBLIC_IP:9000 |
| SONAR_TOKEN | Generated Project Token |

Example

```
SONAR_HOST_URL=http://54.xxx.xxx.xxx:9000

SONAR_TOKEN=xxxxxxxxxxxxxxxxxxxxxxxx
```

---

# Configure Quality Gate

Navigate to:

```
Quality Gates
```

Use the default **Sonar way** Quality Gate or create a custom one based on your project's requirements.

Official Documentation

https://docs.sonarsource.com/sonarqube-server/latest/quality-standards-administration/managing-quality-gates/

---

# Configure Quality Profile

Navigate to:

```
Quality Profiles
```

Use the default language profiles or customize them according to your coding standards.

Official Documentation

https://docs.sonarsource.com/sonarqube-server/latest/quality-standards-administration/managing-quality-profiles/

---

# Sonar Scanner

This project uses the official SonarQube GitHub Action.

Official Documentation

https://docs.sonarsource.com/sonarqube-server/latest/devops-platform-integration/github-integration/

---

# GitHub Actions Workflow

The SonarQube analysis runs automatically after:

- Lint
- GitLeaks
- SAST
- SCA

Before:

- Docker Build
- Trivy Scan
- Deployment

Pipeline Flow

```
Lint
   ↓
GitLeaks
   ↓
SAST
   ↓
SCA
   ↓
SonarQube
   ↓
Docker Build
```

---

# Verify Analysis

After pushing code to the `main` branch:

1. Open GitHub Actions.
2. Wait for the **SonarQube** job to complete.
3. Open the SonarQube dashboard.
4. Review the project analysis.

The dashboard includes:

- Bugs
- Vulnerabilities
- Code Smells
- Security Hotspots
- Coverage (if tests are configured)
- Duplicated Code
- Maintainability Rating
- Reliability Rating

---

# Common Issues

## SonarQube crashes on startup

Cause:

- Insufficient memory.

Solution:

- Use an EC2 instance with at least **8 GB RAM**.

---

## GitHub Action cannot connect to SonarQube

Verify:

- SonarQube service is running.
- Port **9000** is open in the EC2 Security Group.
- `SONAR_HOST_URL` is correct.
- The EC2 Public IP has not changed.
- Firewall rules allow inbound access.

---

## Authentication Failed

Verify:

- `SONAR_TOKEN` is valid.
- The token has not expired.
- The token is stored correctly in GitHub Secrets.

---

## Quality Gate Failed

This means SonarQube detected issues that violate the configured Quality Gate.

Review the dashboard, fix the reported issues, and push your changes again.

---

# Useful Links

SonarQube Documentation

https://docs.sonarsource.com/sonarqube-server/

GitHub Integration

https://docs.sonarsource.com/sonarqube-server/latest/devops-platform-integration/github-integration/

Quality Gates

https://docs.sonarsource.com/sonarqube-server/latest/quality-standards-administration/managing-quality-gates/

Quality Profiles

https://docs.sonarsource.com/sonarqube-server/latest/quality-standards-administration/managing-quality-profiles/

GitHub Actions

https://docs.github.com/actions
