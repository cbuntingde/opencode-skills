---
name: ci-cd-healer
description: Diagnose flaky tests, optimize pipeline caching, and automatically fix common CI/CD failures
license: MIT
compatibility: opencode
metadata:
  audience: devops
  workflow: ci-cd
---

## What I do

I fix CI/CD issues by:

- Diagnosing flaky test patterns
- Identifying and fixing test isolation problems
- Optimizing pipeline caching strategies
- Fixing common build failures
- Suggesting parallelization improvements
- Auto-healing known issues

## When to use me

Use this skill when:
- CI pipelines are failing intermittently
- Tests are flaky or timing-dependent
- Build times are too long
- Pipeline configurations need optimization
- Debugging CI failures

## Usage

```bash
skill ci-cd-healer --diagnose
skill ci-cd-healer --fix-flaky
skill ci-cd-healer --optimize
```

## Diagnosed Issues

I identify and fix:
- Race conditions in tests
- Test order dependencies
- Missing test isolation
- Network call flakiness
- Timer-dependent tests
- Resource contention