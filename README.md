# Homelab Infrastructure

This repository defines my personal homelab stack using Docker Compose.

The repository serves as the source of truth for service definitions and deployment configuration.

## Services

- Traefik (reverse proxy)
- Cloudflared (Cloudflare tunnel ingress)
- Homepage (dashboard)
- Uptime Kuma (monitoring)
- Portainer (container management)
- Actual Budget (finance tracking)
- Reactive Resume (resume management)

## Architecture

All services run on a single Debian VM using Docker Compose.

Stack definitions are organized under:

```text
stacks/<service>/
```

Each service contains its own Docker Compose configuration and required non-sensitive configuration files.

Runtime data, databases, secrets, and generated files are intentionally excluded from Git.

## Workflow

This repository follows a infrastructure-as-code workflow with GitOps principles:

- Git defines infrastructure
- Changes are versioned through commits
- Deployments are reproducible
- Service configuration is managed alongside documentation

To deploy or update a service:

```bash
cd stacks/<service>/
docker compose up -d
```

## Goals

Maintain a simple, reproducible homelab environment where infrastructure changes are:

- documented
- reviewable
- recoverable
- easy to migrate
