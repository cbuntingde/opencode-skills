# Architecture Gatekeeper

Prevent commits that violate architecture patterns or create circular dependencies between modules.

## Overview

The Architecture Gatekeeper skill maintains architectural integrity by analyzing dependencies and blocking changes that violate established patterns. It prevents technical debt accumulation by catching architectural violations before they enter the codebase.

This skill is essential for teams working with layered architectures, domain-driven design, or microservices where strict boundaries must be maintained.

## Usage

### Pre-Commit Check

```bash
skill architecture-gatekeeper --check
```

### Generate Dependency Graph

```bash
skill architecture-gatekeeper --graph --output architecture.svg
```

### Strict Validation

Enable strict mode to fail on any violation:

```bash
skill architecture-gatekeeper --validate --strict
```

### CI Integration

```yaml
# GitHub Actions
- name: Architecture Validation
  run: skill architecture-gatekeeper --check --fail-on violation
```

## Detected Violations

### Circular Dependencies

```
VIOLATION: Circular dependency detected
  src/services/user.ts → src/utils/logger.ts → src/services/user.ts

Solution: Extract logger to a separate module or use dependency injection
```

### Layer Violations

```
VIOLATION: Presentation layer accessing data layer directly
  src/ui/components/UserForm.tsx imports src/db/repositories/UserRepository.ts

Allowed dependencies:
  UI → Services → Repositories → Models
  UI → Models
  Services → Models

Not allowed:
  UI → Repositories
  UI → DB
  Services → UI
```

### Boundary Violations

```
VIOLATION: Core domain module importing infrastructure
  src/domain/User.ts imports src/infrastructure/EmailService.ts

Domain layer should only depend on other domain modules
Move EmailService to domain layer or use dependency inversion
```

## Architecture Definitions

Configure allowed dependencies in `.architecture.yaml`:

```yaml
layers:
  - name: presentation
    patterns:
      - "src/ui/**"
      - "src/components/**"
  - name: application
    patterns:
      - "src/services/**"
      - "src/use-cases/**"
  - name: domain
    patterns:
      - "src/domain/**"
      - "src/entities/**"
  - name: infrastructure
    patterns:
      - "src/repositories/**"
      - "src/db/**"

rules:
  - from: presentation
    to:
      - application
      - domain
      - presentation
  - from: application
    to:
      - domain
      - infrastructure
      - application
  - from: domain
    to:
      - domain
  - from: infrastructure
    to:
      - domain
      - infrastructure

forbidden_patterns:
  - name: No DI in constructors
    pattern: "new \\w+\\("
    layers: [domain]
```

## Requirements

- OpenCode agent environment
- Project structure follows defined layers