# Troubleshooting Guide

This document lists common issues encountered while building and running this project, along with their solutions.

---

# GitHub Actions

## Password required (Docker Login)

### Error

```
Error: Password required
```

### Solution

- Verify `DOCKERHUB_USERNAME`
- Verify `DOCKERHUB_TOKEN`
- Store them in **GitHub Secrets**, not Variables.

---

## Missing test script

### Error

```
npm ERR! Missing script: test
```

### Solution

The frontend currently has no automated tests.

Either:

- Remove the test workflow
- Add Jest/Vitest and define a `test` script in `package.json`

---

## Semgrep fails

### Error

```
Found blocking rule
```

### Solution

For learning:

```yaml
continue-on-error: true
```

For production:

Remove `continue-on-error` and fix the reported issues.

---

## Trivy Action Version

### Error

```
Unable to resolve action
```

### Solution

Always use the latest stable release from the official repository.

https://github.com/aquasecurity/trivy-action

---

## Hadolint Warnings

### Example

```
DL3008
```

### Solution

Pin package versions and use:

```
--no-install-recommends
```

Official Documentation

https://github.com/hadolint/hadolint

---

# SonarQube

## SonarQube Crashes

### Cause

Insufficient RAM.

### Solution

Use at least

- 8 GB RAM
- t3.large AWS instance

---

## Authentication Failed

Verify

- SONAR_TOKEN
- SONAR_HOST_URL

---

# Docker

## Build Failed

Check

```bash
docker build .
```

---

## Login Failed

```bash
docker login
```

Verify Docker Hub credentials.

---

# Deployment

## Runner Offline

Check

```bash
sudo ./svc.sh status
```

Restart

```bash
sudo ./svc.sh restart
```

---

## Deployment Failed

Check

```bash
docker compose logs
```

Verify

- Docker running
- Images exist
- Secrets configured

---

# OWASP ZAP

## Cannot Reach Target

Verify

- Application is running
- Port 80 is open
- Correct target URL
- Security Group allows HTTP

---

# Helpful Commands

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

```bash
docker system prune
```

---

# Official Documentation

GitHub Actions

https://docs.github.com/actions

Docker

https://docs.docker.com

SonarQube

https://docs.sonarsource.com/

OWASP ZAP

https://www.zaproxy.org/docs/
