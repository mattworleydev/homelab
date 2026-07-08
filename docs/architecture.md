# Homelab Architecture

## Overview
This homelab runs on a single Debian VM with Docker Compose.

All service definitions are managed through this repository and deployed from:

```text
/home/matt/homelab/stacks
```

## Core Services

### Networking and Access

- Traefik - Reverse proxy and TLS termination
- Cloudflared - Secure tunnel ingress through Cloudflare

### Management

- Homepage - Homelab dashboard
- Portainer - Container management
- Uptime Kuma - Service monitoring

### Applications

- Actual Budget - Personal finance management
- Reactive Resume - Resume management

## Repository Layout

```text
homelab/
├── docs/
├── scripts/
└── stacks/
├── actualbudget/
├── cloudflared/
├── homepage/
├── portainer/
├── reactive-resume/
├── traefik/
└── uptime-kuma/
```

Each stack contains its Docker Compose definition and required configuration.

## Data Management

Persistent application data is stored outside of Git.

Examples:

- databases
- application state
- uploaded files
- generated certificates
- secrets

These are backed up separately from the repository.

## Deployment Model

The repository follows a GitOps-style approach:

- Git is the source of truth
- Infrastructure changes are committed and versioned
- Deployments are performed from repository definitions
- Services can be recreated consistently on new infrastructure
