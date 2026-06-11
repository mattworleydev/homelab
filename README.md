# Homelab Infrastructure

This repository defines my personal homelab stack using Docker Compose.

## Services

- Traefik (reverse proxy)
- Cloudflared (Cloudflare tunnel ingress)
- Homepage (dashboard)
- Uptime Kuma (monitoring)
- Portainer (container management)
- Actual Budget (finance tracking)

## Architecture

All services run on a single Debian VM using Docker Compose under `/opt/stacks`.

This repository mirrors that directory and will eventually become the source of truth for deployments.

## Goal

Move toward a GitOps-style workflow where:
- Git defines infrastructure
- Changes are versioned
- Deployments are reproducible
