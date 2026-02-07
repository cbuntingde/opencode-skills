---
name: architecture-gatekeeper
description: Prevent commits violating architecture patterns or creating circular dependencies between modules
license: MIT
compatibility: opencode
metadata:
  audience: architects
  workflow: code-review
---

## What I do

I enforce architectural boundaries by:

- Detecting and preventing circular dependencies
- Validating layer adherence (e.g., data access not calling presentation)
- Enforcing module boundaries and interfaces
- Preventing cross-layer violations
- Blocking architecture anti-patterns
- Generating dependency graphs for visualization

## When to use me

Use this skill when:
- Setting up architecture enforcement in CI/CD
- Onboarding new team members
- Refactoring legacy monoliths
- Enforcing clean architecture patterns
- Validating microservice boundaries

## Usage

```bash
skill architecture-gatekeeper --check
skill architecture-gatekeeper --graph
skill architecture-gatekeeper --validate --strict
```

## Enforced Patterns

- Layered architecture (presentation → business → data)
- Dependency direction (abstractions should not depend on concretions)
- Module isolation (no circular imports/references)
- Boundary enforcement (domain layer has no external dependencies)