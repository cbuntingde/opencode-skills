# Codebase Cartographer

Visualize architectural boundaries and dependency relationships in your codebase.

## Overview

Codebase Cartographer analyzes the structure of a codebase to generate visual architectural diagrams. It identifies modules, layers, and dependency patterns, helping developers understand system architecture, spot boundary violations, and plan refactoring efforts.

This skill is invaluable when:
- Onboarding to a new codebase and need a quick overview
- Reviewing architecture during code review
- Documenting existing systems for stakeholders
- Planning refactoring by visualizing current state
- Identifying tight coupling or circular dependencies

## Usage

### Prerequisites

- OpenCode CLI tool installed
- Read permissions for the target codebase
- Bash access for file exploration and analysis

### Installation

**Global Installation:**
```bash
cp -r codebase-cartographer ~/.config/opencode/skills/
```

**Project Installation:**
```bash
mkdir -p .opencode/skills
cp codebase-cartographer/* .opencode/skills/
```

### Invocation

Invoke the skill using OpenCode:

```
@codebase-cartographer Map the architecture of this codebase
@codebase-cartographer Visualize module boundaries and dependencies
@codebase-cartographer Find circular dependencies in src/
@codebase-cartographer Identify architectural patterns in this project
@codebase-cartographer Document the current architecture
```

## Examples

### Example 1: Analyze New Codebase

**Prompt:**
```
@codebase-cartographer Map the architecture of this project
```

**Output:**
```
CODEBASE STRUCTURE
==================

src/
├── api/              # REST/HTTP layer
│   ├── routes/
│   ├── controllers/
│   └── middleware/
├── core/             # Domain logic
│   ├── entities/
│   ├── services/
│   └── repositories/
├── infrastructure/   # External integrations
│   ├── database/
│   ├── cache/
│   └── messaging/
└── utils/            # Shared utilities

ARCHITECTURAL STYLE: Layered Architecture

DEPENDENCY ANALYSIS
===================

Dependency Flow (clean):
  api → core → infrastructure

Cross-cutting concerns:
  - utils/ is referenced by all layers (coupling risk)
  - infrastructure/ referenced by api/ (boundary violation)

ISSUES FOUND
============

1. CRITICAL: Circular dependency detected
   core/services/auth ↔ infrastructure/security

2. MEDIUM: Boundary violation
   api/ imports infrastructure/database directly

3. LOW: Tight coupling via utils/
   12 files across modules depend on utils/

RECOMMENDATIONS
===============

1. Break circular dependency by extracting shared interface
2. Enforce layer boundaries with module boundaries
3. Consider extracting core utilities into separate package
```

### Example 2: Identify Architectural Patterns

**Prompt:**
```
@codebase-cartographer What architectural pattern does this codebase follow?
```

**Output:**
```
DETECTED PATTERN: Ports and Adapters (Hexagonal)

Evidence:
  - core/ defines interfaces (ports)
  - infrastructure/ implements external concerns (adapters)
  - api/ is a primary adapter for HTTP
  - clear dependency direction: core ← adapters

MODULE ROLES:
  - core: Application business logic (domain)
  - ports: Interface definitions
  - adapters: External system integrations

COUPLING ASSESSMENT: Good separation of concerns
```

### Example 3: Find Dependency Issues

**Prompt:**
```
@codebase-cartographer Find all circular dependencies and boundary violations
```

**Output:**
```
DEPENDENCY ANALYSIS REPORT
==========================

CIRCULAR DEPENDENCIES (2 found):
=================================

1. users/ ↔ auth/
   users/service.ts → auth/token.ts
   auth/manager.ts → users/repository.ts

2. data/ ↔ sync/
   data/cache.ts → sync/handler.ts
   sync/manager.ts → data/store.ts

BOUNDARY VIOLATIONS (5 found):
===============================

1. api/ → database/
   Violates: Presentation → Infrastructure

2. core/ → filesystem/
   Violates: Domain → Infrastructure

3. services/ → external-api/
   Violates: Application → External

VIOLATIONS BY LAYER:
  - Presentation: 2 violations
  - Application: 1 violation
  - Domain: 1 violation
  - Infrastructure: 0 violations
```

## Configuration

No configuration required. The skill automatically analyzes the codebase structure and dependencies.

### Optional Analysis Targets

You can specify target directories:

```
@codebase-cartographer Analyze src/domain/ only
@codebase-cartographer Map tests/ architecture
@codebase-cartographer Visualize lib/ dependencies
```

### Output Customization

Request specific output formats:

```
@codebase-cartographer Generate ASCII diagram only
@codebase-cartographer List dependency violations summary
@codebase-cartographer Output JSON dependency graph
```

## Requirements

- **OpenCode**: CLI tool version supporting skill framework
- **Bash**: For directory traversal and file analysis
- **Read Access**: Permission to read all code files in target directory

### Supported Languages

Best support for:
- TypeScript/JavaScript
- Python
- Java
- Go
- Rust

Limited support for:
- Ruby
- PHP
- Other languages with import-based dependency structures

### Performance Notes

- Small codebases (<1000 files): Complete analysis in seconds
- Medium codebases (1000-10000 files): Analysis in 10-30 seconds
- Large codebases (>10000 files): May take 1-2 minutes

## Related Skills

- **style-mimic**: For maintaining coding style consistency
- **code-review**: For detailed code quality feedback
- **qa-skill**: For comprehensive quality assurance

## License

MIT