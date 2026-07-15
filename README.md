# Homelab Infrastructure

This repository defines my personal homelab infrastructure using Docker Compose and Infrastructure-as-Code principles.

The goal of this project is to build a reproducible, documented, and maintainable environment while developing practical experience with:

- Infrastructure as Code
- GitOps workflows
- Secret management
- Containerization
- Reverse proxying
- Secure remote access
- Monitoring and observability

This repository serves as the source of truth for service definitions, configuration, and documentation.

## Current Services

### Networking and Access

- Traefik - Reverse proxy and TLS termination
- Cloudflared - Secure Cloudflare Tunnel ingress

### Management and Operations

- Homepage - Homelab dashboard
- Portainer - Container management
- Uptime Kuma - Service monitoring

### Security and Secrets

- Vaultwarden - Password management
- Infisical - Secrets management platform

### Applications

- Actual Budget - Personal finance management
- Reactive Resume - Resume management

## Architecture

This homelab currently runs on a Debian VM using Docker Compose.

Each service is organized as an independent stack:

```text
stacks/<service>/
```

Example:

```text
stacks/
├── actualbudget/
│   └── compose.yml
├── cloudflared/
│   └── compose.yml
├── homepage/
│   ├── compose.yml
│   └── config/
├── infisical/
│   └── compose.yml
├── portainer/
│   └── compose.yml
├── reactive-resume/
│   ├── compose.yml
│   └── .env
├── traefik/
│   ├── compose.yml
│   └── data/
├── uptime-kuma/
│   └── compose.yml
└── vaultwarden/
    └── compose.yml
```

Each stack contains its Docker Compose definition and required non-sensitive configuration files.

Runtime data, databases, secrets, certificates, and generated files are intentionally excluded from Git.

## Infrastructure Principles

This repository follows Insfrastructure as Code (IaC) and GitOps principles:

- Infrastructure configuration is stored in Git
- Changes are tracked through commits
- Service definitions are managed declaratively
- Infrastructure decisions are documented
- Deployments can be reproduced from repository files

The current deployment process is manual Docker Compose deployment, with future goals of introducing additional automation.

## Secrets Management

Sensitive information is intentionally separated from source control.

Current approach:

- Infisical manages application and infrastructure secrets
- Vaultwarden manages human passwords and credentials
- Secrets and sensitive files are excluded from Git

The long-term goal is to integrate centralized secret management with automated deployment workflows.

## Data Management

Persisted application data is stored separately from Git.

Examples:

- Databases
- Uploaded files
- Application state
- Generated certificates
- Runtime logs
- Backups

Application data is backed up independently from the repository.

## Workflow

To deploy or update a service:

```bash
cd stacks/<service>/
docker compose up -d
```

After making infrastructure changes:

```bash
git add .
git commit -m "Describe infrastructure change"
git push
```

## Goals

Maintain a simple, reproducible homelab environment where infrastructure changes are:

- documented
- reviewable
- recoverable
- secure
- easy to migrate

Long-term goals include:

- expanding GitOps automation
- improving configuration management
- automating deployments
- improving monitoring and observability
