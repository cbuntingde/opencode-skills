# Environment Guard

Block dangerous operations in production environments and validate environment-specific configurations.

## Overview

The Environment Guard skill protects production systems by detecting the current environment and blocking or alerting on potentially destructive operations. It serves as a safety net to prevent costly mistakes that could cause downtime or data loss.

This skill is essential for teams managing multiple environments where the same commands might be safe in development but catastrophic in production.

## Usage

### Environment Detection

```bash
skill environment-guard --check
Current environment: production
```

### Block Destructive Operations

```bash
skill environment-guard --block-destroy
```

### Validate Configuration

```bash
skill environment-guard --validate-config
```

### Guard a Command

```bash
skill environment-guard --run "npm run migrate"
```

## Protected Operations

### Blocked in Production

| Operation | Safety Level |
|-----------|-------------|
| `TRUNCATE TABLE` | Requires --force flag |
| `DROP DATABASE` | Blocked completely |
| `DELETE *` | Requires --dry-run first |
| `redis FLUSHALL` | Blocked completely |
| `rm -rf` | Requires explicit path validation |

### Warning Operations

| Operation | Alert |
|-----------|-------|
| Service restart | Logs to monitoring |
| Configuration change | Requires approval |
| Secret rotation | Requires backup |
| Scaling operations | Logs to audit trail |

## Environment Detection

Detects environment from:
- `NODE_ENV`, `ENV`, `RAILS_ENV` environment variables
- Git branch name
- Kubernetes namespace
- AWS/GCP region or tag
- Custom environment markers

## Configuration

Create `.environment-guard.yaml`:

```yaml
environments:
  production:
    patterns:
      - "prod*"
      - "production"
    blocking:
      - truncate
      - drop
      - flush
    warning:
      - restart
      - scale
      - secret-rotation

  staging:
    patterns:
      - "staging"
      - "pre-prod"
    blocking:
      - truncate
      - drop
    warning:
      - flush

whitelist:
  commands:
    - "npm run safe-migrate"
    - "python manage.py cleanup"

required_flags:
  truncate: --dry-run
  delete: --confirm
```

## Safety Levels

### Strict Mode (Production)

```bash
skill environment-guard --strict
# All dangerous operations blocked
```

### Audit Mode

```bash
skill environment-guard --audit
# Operations logged but not blocked
```

### Warning Mode

```bash
skill environment-guard --warn
# Confirmation prompts for dangerous operations
```

## Requirements

- OpenCode agent environment
- Access to environment variables
- Optional: access to deployment metadata