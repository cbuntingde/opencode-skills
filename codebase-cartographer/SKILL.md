---
name: codebase-cartographer
description: Generate visual architectural diagrams and maps of codebase structure, identifying modules, dependencies, boundaries, and architectural patterns
license: MIT
compatibility: opencode
metadata:
  audience: architects
  workflow: analysis
---

## What I do

- Analyze codebase directory structure and organization
- Identify module boundaries and architectural layers
- Map import/export relationships and dependency direction
- Detect circular dependencies and coupling issues
- Generate ASCII architecture diagrams
- Identify patterns: layered, hexagonal, microservices, monolith
- Document architectural decisions and component relationships
- Flag potential refactoring needs (tight coupling, God objects)

## When to use me

Use this when you need to:
- Understand a new codebase's structure
- Document existing architecture for onboarding
- Identify architectural boundaries violations
- Plan refactoring by visualizing current state
- Onboard to unfamiliar codebases quickly
- Review architecture during code review
- Create architecture documentation for stakeholders

## How I work

1. **Scan codebase structure** - Walk directory tree to identify module organization
2. **Analyze dependencies** - Parse import statements to map relationships
3. **Detect patterns** - Identify architectural styles from structure and dependencies
4. **Generate visualization** - Create ASCII diagrams showing modules and dependencies
5. **Report findings** - Provide architectural assessment with recommendations

## Output format

I provide:

1. **ASCII dependency graph** showing modules and relationships
2. **Layer analysis** showing architectural boundaries
3. **Dependency direction** indicating coupling quality
4. **Anti-pattern detection** highlighting architectural problems
5. **Recommendations** for improving architectural boundaries

Example output:

```
src/
├── api/           # HTTP layer
├── domain/        # Business logic
├── infrastructure/# External concerns
└── utils/         # Shared utilities

Dependency Analysis:
  api → domain (clean)
  domain → infrastructure (clean)
  utils is shared - potential coupling risk

Issues found:
  - Circular dependency: infrastructure/auth ↔ services/user
  - domain/ references infrastructure/ directly (boundary violation)
```

## Limitations

- Analyzes structure, not business logic correctness
- Language support varies (best for TS/JS, Python, Java)
- Does not modify code, only visualizes existing structure
- Large codebases may produce complex diagrams