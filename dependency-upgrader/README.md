# Dependency Upgrader

Safely upgrade project dependencies while managing breaking changes and security updates.

## Overview

The Dependency Upgrader skill manages dependency updates across your project with safety mechanisms that prevent breaking changes from reaching production. It analyzes version ranges, detects breaking changes, runs compatibility tests, and provides migration strategies for complex upgrades.

This skill reduces the maintenance burden of keeping dependencies current while minimizing the risk of introducing regressions.

## Usage

### Scan for Updates

```bash
skill dependency-upgrader --scan
```

### Safe Upgrade (Minor/Patch)

```bash
skill dependency-upgrader --upgrade
```

### Major Version Upgrade with Analysis

```bash
skill dependency-upgrader --major --analyze
```

### Security Updates Only

```bash
skill dependency-upgrader --security
```

### Specific Package Upgrade

```bash
skill dependency-upgrader --package react --target 18.2.0
```

## Workflow

### 1. Scan Phase

The skill scans your dependency files and compares against:

- npm registry / PyPI / crates.io
- GitHub changelogs
- Security advisories (GitHub, Snyk, npm audit)
- Deprecation notices

### 2. Impact Analysis

For each upgrade, the skill analyzes:

- Breaking change indicators in changelogs
- Usage of affected APIs in your codebase
- Test coverage for affected modules
- Downstream dependency compatibility

### 3. Migration Planning

Generates a migration plan with:

- Required codemods and their sources
- Compatibility layer installations
- Code changes needed for breaking changes
- Estimated effort and risk level

### 4. Execution

Safely applies upgrades with:

- Backup of package.json and lockfile
- Dry-run mode for review
- Automatic test running
- Rollback capability on failure

## Example Output

### Scan Results

```
Dependency Report
=================

Critical (Security):
  lodash < 4.17.21 - CVE-2021-23337
  axios < 0.21.1 - SSRF vulnerability

Outdated:
  react 17.0.2 -> 18.2.0 (major)
  typescript 4.5.0 -> 5.0.0 (major)

Safe to upgrade:
  chalk 4.1.0 -> 4.1.2
  uuid 8.3.2 -> 8.3.2 (already latest)
```

### Migration Plan for React 18

```
Migration: react 17 -> 18
================================

Breaking Changes:
1. New JSX Transform (automatic)
   Action: None required for React 17+

2. Strict Effects StrictMode double-mount
   Action: Ensure effects are resilient to double-invocation
   Files affected: src/hooks/useAnalytics.ts

3. Dropped support for old event types
   Action: Migrate onMouseWheel -> onWheel
   Codemod: npx react-codemod update-event-types

Scripts to run:
  npm install react@18 react-dom@18
  npx react-codemod update-event-types
  npm test
```

## Configuration

### Upgrade Strategy

```json
{
  "strategy": "safe",
  "includeSecurity": true,
  "includeDeprecations": true,
  "majorVersions": {
    "react": "ask",
    "typescript": "ask",
    "eslint": "auto"
  },
  "lockfile": "preserve",
  "autoTest": true
}
```

### Package Manager

```json
{
  "manager": "npm",
  "alternatives": ["yarn", "pnpm"]
}
```

### Custom Registry

```json
{
  "registry": "https://registry.npmjs.org",
  "timeout": 30000
}
```

## Supported Package Managers

| Manager | Lockfile | Files |
|---------|----------|-------|
| npm | package-lock.json | package.json |
| yarn | yarn.lock | package.json |
| pnpm | pnpm-lock.yaml | package.json |
| pip | requirements.lock | requirements.txt |
| go | go.sum | go.mod |
| cargo | Cargo.lock | Cargo.toml |

## Codemod Integration

The skill integrates with community codemods for major upgrades:

| Package | Codemod |
|---------|---------|
| React 17 -> 18 | react-codemod |
| Angular 14 -> 15 | ng-update |
| Vue 2 -> 3 | vue-codemod |
| TypeScript | ts-migrate |

## Best Practices

### Automated Security Updates

```bash
# Run weekly
0 0 * * 0 skill dependency-upgrader --security --auto
```

### Pre-Release Testing

```bash
# Test in CI before merging
skill dependency-upgrader --upgrade --dry-run
npm test
```

### Selective Upgrades

```bash
# Only safe updates in production branches
skill dependency-upgrader --safe --exclude major
```

## Requirements

- Node.js 14+ for npm/yarn/pnpm
- Python 3.8+ for pip
- Go 1.18+ for Go modules
- Cargo for Rust projects
- Git for version control