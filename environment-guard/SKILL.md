---
name: environment-guard
description: Block dangerous operations in production environments and validate environment-specific configurations
license: MIT
compatibility: opencode
metadata:
  audience: devops
  workflow: deployment
---

## What I do

I protect production environments by:

- Detecting when running in production
- Blocking dangerous operations (truncation, destructive queries)
- Validating environment-specific configurations
- Requiring confirmation for irreversible actions
- Alerting on missing safety checks
- Enforcing environment gates

## When to use me

Use this skill when:
- Preventing accidental production data loss
- Blocking dangerous migrations in production
- Ensuring required safeguards are in place
- Validating environment-specific settings
- Auditing environment access patterns

## Usage

```bash
skill environment-guard --check
skill environment-guard --block-destroy
skill environment-guard --validate-config
```

## Protected Operations

I block or require confirmation for:
- Database truncation or drop operations
- File system destructive operations
- Cache clearing in production
- Secret rotation without backup
- Service restart in production
- Migration without rollback plan