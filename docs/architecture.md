# Homelab Architecture

## Overview
This homelab runs on a single Debian VM with Docker Compose.

## Core Services
- Traefik (reverse proxy)
- Cloudflared (tunnel to Cloudflare)
- Homepage (dashboard)
- Uptime Kuma (monitoring)
- Portainer (container management)
- Actual Budget (finance app)

## Layout
All services are defined in /opt/stacks and mirrored in this repository.

## Goal
Move toward GitOps-based deployment where Git is the source of truth.
