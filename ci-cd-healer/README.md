# CI/CD Healer

Diagnose and automatically fix flaky tests, optimize pipeline caching, and resolve common CI/CD failures.

## Overview

The CI/CD Healer skill diagnoses issues in continuous integration and deployment pipelines. It identifies the root cause of failures and provides automated fixes for common problems like flaky tests, inefficient caching, and configuration issues.

This skill is essential for teams struggling with unreliable CI pipelines that slow down development velocity.

## Usage

### Diagnose Pipeline Issues

```bash
skill ci-cd-healer --diagnose
```

### Fix Flaky Tests

```bash
skill ci-cd-healer --fix-flaky
```

### Optimize Pipeline

```bash
skill ci-cd-healer --optimize
```

### Analyze Specific Failure

```bash
skill ci-cd-healer --analyze "test-failure.log"
```

## Detected Issues

### Test Flakiness

| Issue | Root Cause | Fix |
|-------|-----------|-----|
| Tests pass locally, fail in CI | Race condition | Add test isolation |
| Intermittent timeout failures | Timer dependency | Mock timers |
| Tests depend on execution order | No cleanup between tests | Setup/teardown |
| Network calls fail randomly | No retries | Add retry logic |

### Pipeline Inefficiency

| Issue | Impact | Fix |
|-------|--------|-----|
| No dependency caching | +5 min per run | Add cache configuration |
| Sequential test runs | +10 min per run | Enable parallelization |
| Large artifact uploads | +2 min per run | Selective artifact upload |
| No incremental builds | +3 min per run | Configure incremental build |

### Build Failures

| Issue | Root Cause | Fix |
|-------|-----------|-----|
| Node version mismatch | Wrong engine | Specify engine version |
| Missing dependency | Race condition | Add npm install retry |
| Permission denied | CI context | Fix file permissions |
| Memory exhausted | Heavy process | Increase memory limit |

## Example Diagnosis

```
[CI/CD DIAGNOSIS]

ISSUE: Flaky integration tests in ci/test-e2e.js

Root Causes:
1. Tests share database state without cleanup
2. Network calls have no retry logic
3. Tests depend on execution order

Recommended Fixes:
1. Add beforeEach/afterEach cleanup
2. Implement exponential backoff retry
3. Randomize test order
4. Use test database per suite

APPLY FIXES? [y/N]
```

## Pipeline Optimization

Before optimization:
```
Total build time: 12:34
  - Install dependencies: 2:15
  - Run tests: 8:20
  - Build artifacts: 1:59
```

After optimization:
```
Total build time: 4:21
  - Install dependencies: 0:45 (cached)
  - Run tests: 2:40 (parallelized)
  - Build artifacts: 0:56 (incremental)

Savings: 8:13 (66% reduction)
```

## Configuration

Create `.ci-cd-healer.yaml`:

```yaml
analysis:
  flaky_tests: true
  caching: true
  parallelization: true
  build_optimization: true

fixes:
  auto_apply: false
  create_pr: true
  commit_message: "ci: fix flaky tests"

caching:
  strategies:
    - pattern: "**/node_modules/**"
      key: "package-lock.json"
    - pattern: "**/.gradle/**"
      key: "gradle.lockfile"

parallelization:
  test_threads: 4
  max_parallel_jobs: 8
```

## Requirements

- OpenCode agent environment
- CI/CD configuration file access
- Test framework available