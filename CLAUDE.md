# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

This is a Helm charts repository containing 35+ charts for Mina Protocol ecosystem applications and infrastructure components. Each chart follows a standardized structure with:
- `Chart.yaml` - Chart metadata and versioning
- `values.yaml` - Default configuration values with extensive documentation comments
- `README.md` - Auto-generated documentation from values.yaml using helm-docs
- `templates/` - Kubernetes YAML templates
- `README.md.gotmpl` - Template for generating README files

## Key Charts Categories

**Mina Protocol Core:**
- `mina-daemon` - Core Mina Protocol daemon
- `mina-archive` - Blockchain archive service
- `mina-rosetta` - Rosetta API implementation
- `mina-mesh` - Mina Mesh service

**Monitoring & Analytics:**
- `node-stats-collector` - Node statistics collection
- `mina-alerts` - Monitoring alerts
- `block-producers-uptime-monitoring` - Uptime tracking
- `minametrix` - Metrics and analytics

**Governance & Delegation:**
- `delegation-program-leaderboard` - Delegation leaderboard
- `delegation-verify-coordinator` - Delegation verification
- `on-chain-voting` - Governance voting system
- `pgt-*` - Protocol Governance Token related services

**OpenMina Ecosystem:**
- `openmina-node` - OpenMina node implementation
- `openmina-frontend` - OpenMina web interface
- `openmina-block-producer-dashboard` - Block producer dashboard
- `openmina-p2p-replayer` - P2P network replayer

## Common Development Commands

### Chart Development
```bash
# Install pre-commit hooks (required for contributions)
pre-commit install
pre-commit install-hooks

# Generate/update README files from values.yaml comments
helm-docs

# Validate chart syntax
helm lint <chart-name>

# Template chart to see generated Kubernetes resources
helm template <release-name> <chart-name>

# Install chart locally
helm install <release-name> ./<chart-name>

# Package chart for distribution
helm package <chart-name>
```

### Working with Values Files
The `values.yaml` files use a specific commenting convention for auto-generating documentation:
- `# -- Description` - Documents the configuration option
- Comments must be placed directly above the configuration key
- Use meaningful descriptions as they become part of the generated README

### Testing and Deployment
```bash
# Use helmfile for complex deployments
helmfile template    # Generate resources
helmfile apply       # Deploy to cluster
helmfile status      # Check deployment status

# Alternative kubectl deployment
helmfile template | kubectl apply -f -
```

## Architecture Notes

**Chart Structure:** Each chart is self-contained with its own values, templates, and documentation. Charts can have dependencies defined in Chart.yaml.

**Values Organization:** Values are hierarchically organized with deployment-specific settings at the top level and service-specific configurations nested below.

**Template Patterns:** Charts use common Kubernetes patterns with ConfigMaps, Secrets, Deployments, Services, and Ingress resources. Many charts support optional features like monitoring, persistence, and autoscaling.

**Documentation Generation:** READMEs are auto-generated from values.yaml comments using helm-docs with the README.md.gotmpl template, ensuring documentation stays in sync with configuration options.

**Pre-commit Workflow:** The repository enforces documentation generation and shell script validation through pre-commit hooks, ensuring consistency and quality.