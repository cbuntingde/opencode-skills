---
name: code-policy-enforcer
description: Enforce team-specific coding standards, architectural boundaries, and forbidden patterns across the codebase
license: MIT
compatibility: opencode
metadata:
  audience: tech-leads
  workflow: code-quality
---

## What I do

I enforce code policies by:

- Validating team-specific coding standards
- Checking architectural boundaries
- Identifying forbidden patterns
- Ensuring documentation requirements
- Verifying test coverage thresholds
- Blocking violations before merge

## When to use me

Use this skill when:
- Establishing team coding standards
- Enforcing architectural patterns
- Preventing known anti-patterns
- Requiring documentation and tests
- Creating quality gates for PRs

## Usage

```bash
skill code-policy-enforcer --check
skill code-policy-enforcer --enforce
skill code-policy-enforcer --list-rules
```

## Enforced Policies

I enforce:
- Code style guidelines
- Complexity thresholds
- Documentation requirements
- Test coverage minimums
- Import patterns
- Forbidden language features
- Security patterns