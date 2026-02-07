# Code Policy Enforcer

Enforce team-specific coding standards, architectural boundaries, and forbidden patterns across the codebase.

## Overview

The Code Policy Enforcer skill ensures consistent code quality by enforcing team-defined policies. It validates code against configurable rules, blocking violations before they enter the codebase.

This skill is essential for teams that want to maintain code quality without relying solely on manual code review.

## Usage

### Check Current Changes

```bash
skill code-policy-enforcer --check
```

### Enforce Strict Mode

```bash
skill code-policy-enforcer --enforce
```

### List Active Rules

```bash
skill code-policy-enforcer --list-rules
```

### CI Integration

```yaml
# GitHub Actions
- name: Code Policy Check
  run: skill code-policy-enforcer --enforce --fail-on violation
```

## Policy Categories

### Code Style
- Naming conventions (camelCase, PascalCase, etc.)
- Indentation and formatting
- Line length limits
- Import organization
- File structure

### Complexity Limits
- Maximum cyclomatic complexity: 10
- Maximum function length: 30 lines
- Maximum file length: 300 lines
- Maximum parameters: 4

### Documentation Requirements
- Public functions require JSDoc/TSDoc
- Complex logic requires inline comments
- README updates for new features
- API documentation for endpoints

### Testing Requirements
- Minimum test coverage: 80%
- Critical paths must have unit tests
- Integration tests for API endpoints
- Edge cases in test scenarios

### Security Patterns
- No hardcoded secrets
- Input validation required
- SQL parameterization enforced
- Authentication on protected endpoints

### Forbidden Patterns
- `console.log` in production code
- `any` type in TypeScript
- Synchronous file operations in async handlers
- Floating promises
- Empty catch blocks

## Example Violation

```
[CODE POLICY VIOLATION]

Rule: no-console-log
Severity: ERROR
File: src/utils/logger.ts:45

Violation: console.log() detected

Fix: Use structured logger instead
  import { logger } from '../utils/logger';
  logger.info('User action logged');
```

## Configuration

Create `.code-policy.yaml`:

```yaml
policies:
  style:
    naming:
      functions: camelCase
      classes: PascalCase
      constants: UPPER_SNAKE_CASE
    formatting:
      indent: 2
      line_length: 100

  complexity:
    max_cyclomatic_complexity: 10
    max_function_lines: 30
    max_file_lines: 300
    max_parameters: 4

  documentation:
    require_jsdoc: true
    require_readme_updates: true

  testing:
    min_coverage: 80
    require_edge_cases: true

  security:
    no_hardcoded_secrets: true
    require_input_validation: true
    require_sql_parameterization: true

  forbidden:
    - pattern: console\.(log|warn|error)
      message: Use structured logger
    - pattern: "as any"
      message: Use proper type guards
    - pattern: "\\.then\\([^)]*\\)"
      message: Handle promise errors

exceptions:
  - file: "**/test/**"
    rules: [style, complexity]
  - file: "**/*.config.js"
    rules: [complexity]
```

## Requirements

- OpenCode agent environment
- Linter configuration (ESLint, etc.)
- Test coverage tool (optional)
- TypeScript compiler (for complexity analysis)