# Homelab Architecture

## Overview
This homelab is built around a virtualization-first architecture.

The current environment consists of:

- Proxmox for virtualization
- Debian VM for Docker workloads
- Docker Compose for service deployment
- GitHub repository for infrastructure configuration

The Docker environment is managed from:

```text
/home/matt/homelab
```

This repository contains service definitions, configuration files, and documentation required to recreate the application layer of the homelab.

## Infrastructure Layout

Current architecture:

```text
Physical Hardware
        |
        v
     Proxmox
        |
        v
 Debian Docker VM
        |
        v
 Docker Compose Stacks
        |
        v
 Application Containers
```

## Docker Stack Organization

Each service is deployed as an independent Docker Compose stack.

Repository structure:

```text
homelab/
├── docs/
│   ├── architecture.md
│   └── rules.md
├── scripts/
└── stacks/
    ├── actualbudget/
    ├── cloudflared/
    ├── homepage/
    ├── infisical/
    ├── portainer/
    ├── reactive-resume/
    ├── traefik/
    ├── uptime-kuma/
    └── vaultwarden/
```

Each stack contains:

- Docker Compose definition
- Service-specific configuration
- Non-sensitive deployment files

Persistent application data is stored separately from the repository.

## Network Architecture

External access is provided through Cloudflare Tunnel.

Current traffic flow:

```text
Internet
    |
    v
Cloudflare
    |
    v
Cloudflare Tunnel
    |
    v
Traefik Reverse Proxy
    |
    v
Docker Services
```

## Reverse Proxy

### Traefik

Traefik is responsible for:

- Reverse proxying services
- TLS termination
- Routing requests to Docker services

Applications are exposed through Traefik rather than directly publishing individual services externally.

## Secure Remote Access

### Cloudflared

Cloudflare provides:

- Secure remote access through Cloudflare Tunnel
- No direct inbound port forwarding
- External routing into the homelab environment

## Service Categories

### Infrastructure Services

#### Traefik

Role:

- Reverse proxy
- TLS management
- Service routing

#### Cloudflared

Role:

- Secure tunnel ingress

### Management Services

#### Homepage

Role:

- Centralized dashboard
- Service navigation
- Homelab overview

#### Portainer

Role:

- Docker management interface

#### Uptime Kuma

Role:

- Service availability monitoring

### Security Services

#### Infisical

Role:

- Application and infrastructure secret management

Infisical is intended to store sensitive configuration values that should not exist in Git.

#### Vaultwarden

Role:

- Human credential management

Vaultwarden stores personal passwords and credentials.

Infisical and Vaultwarden serve different purposes:

| Service | Purpose |
| --- | --- |
| Infisical | Application secrets and infrastructure credentials |
| Vaultwarden | Human-managed passwords |

### Application Services

#### Actual Budget

Role:

- Personal finance management

#### Reactive Resume

Role:

- Resume management

## Data Management

Application runtime data is intentionally separated from source control.

Excluded from Git:

- Databases
- Uploaded files
- Application state
- Secrets
- Certificates
- Logs
- Generated files

Examples:

```text
/data/
*.sqlite
*.db
.env
acme.json
*.pem
```

Persistent data is backed up separately from the Git repository.

## Deployment Workflow

Current deployment process:

```text
GitHub Repository
        |
        v
Manual Docker Compose Deployment
        |
        v
Running Containers
```

Example:

```bash
cd stacks/<services>/
docker compose up -d
```

## Future Improvements

Planned improvements:

- Automated GitOps deployment workflow
- Secret injection from Infisical
- Configuration management using tools such as Ansible
- Improved monitoring and observability
- Automated backup validation
- Disaster recovery procedures
