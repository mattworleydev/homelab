# Homelab Repository Rules

This repository contains declarative infrastructure configuration for the homelab.

The purpose of this repository is to maintain a reproducible, documented, and version-controlled infrastructure environment while preventing sensitive information from being exposed.

## Repository Principles

This repository follows Infrastructure as Code (IaC) principles:

- Infrastructure configuration should be stored as code
- Changes should be tracked through Git history
- Infrastructure decisions should be documented
- Deployments should be reproducible
- Sensitive information should remain outside source control

## Allowed Files

The following files may be committed:

- Docker Compose files
- Service configuration files
- Documentation
- Deployment scripts
- Non-sensitive configuration
- Homepage dashboard configuration
- Reverse proxy configuration

Examples:

```text
compose.yml
traefik.yml
config.yml
services.yaml
README.md
architecture.md
```

## Restricted Files

The following should never be committed:

- Secrets
- Passwords
- API keys
- Tokens
- Private keys
- Environment files containing credentials
- Databases
- Application runtime data
- Logs
- Generated files

Examples:

```text
.env
*.sqlite
*.db
*.pem
/data/
logs/
acme.json
```

## Secret Management

Secrets should be managed separately from Git.

Current tools:

- Infisical - Application and infrastructure secrets
- Vaultwarden - Human passwords and credentials

Sensitive values should never be hardcoded into:

- Docker Compose files
- Configuration files
- Scripts
- Documentation

When a service requires secrets:

1. Store the secret in the appropriate secret management system
2. Reference the secret through environment variables or secure injection methods
3. Verify that sensitive values are excluded from Git


## Data Management

Persistent application data should remain separate from repository files.

Examples:

- Databases
- Uploaded documents
- Media libraries
- Application state
- Backups
- Certificates

Application data should be backed up independently from source control.

## Service Standards

Each service should have its own directory:

```text
stacks/<service>/
```

Each stack should contain:

- `compose.yml`
- Required non-sensitive configuration
- Documentation if needed

Services should avoid unnecessary coupling with other stacks.

## Change Process

Infrastructure changes should follow this process:

1. Make changes in the repository
2. Test changes locally
3. Review changes with Git diff
4. Commit changes with a descriptive message
5. Push changes to GitHub
6. Deploy the updated configuration

Example:

```bash
git add .
git commit -m "Add service configuration"
git push
```

## Documentation Requirements

Documentation should be updated when:

- Adding new services
- Changing architecture
- Changing security practices
- Changing deployment processes

The goal is that another person can understand the environment without relying on undocumented knowledge.

## Future Automation

Future improvements may include:

- Automated GitOps deployments
- Secret injection workflows
- Configuration management
- Automated backups
- Disaster recovery testing
