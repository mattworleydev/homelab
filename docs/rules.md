# Homelab Repo Rules

This repository contains declarative infrastructure configuration for the homelab.

The goal is to keep deployments reproducible while avoiding storing sensitive or generated data.

## Allowed

The following may be committed:

- Docker Compose files
- Reverse proxy configuration
- Application configuration files
- Documentation
- Deployment scripts
- Non-sensitive static configuration

Examples:

- `compose.yml`
- Traefik configuration
- Homepage YAML files

## Not allowed

The following should not be committed:

- Secrets
- Environment files containing credentials
- API tokens
- Private keys
- Databases
- Runtime application data
- Logs
- Generated files

Examples:

```text
.env
*.sqlite
*.db
/data/
logs/
acme.json
```

## Data Handling

Persistent application data must be stored separately from the Git repository.

Backups of application data should be handled independently from source control.

## Changes

Infrastructure changes should:

1. Be made in the repository
2. Be reviewed through Git history
3. Be deployed from the updated stack definition
4. Include documentation updates when architecture changes
