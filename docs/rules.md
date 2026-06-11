# Homelab Repo Rules

This repository contains ONLY declarative configuration for services.

## Allowed
- docker-compose.yml files
- reverse proxy config (Traefik)
- application config (Homepage, etc.)

## Not allowed
- databases (*.sqlite, *.db)
- runtime data (/data folders)
- secrets (.env files)
- logs
