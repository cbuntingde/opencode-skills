# Code Review Automation

Automate code review workflows by analyzing pull requests against team standards and identifying issues.

## Overview

The Code Review Automation skill provides systematic code review analysis that complements human reviewers. It catches issues that are tedious to check manually, ensuring consistent quality standards across all pull requests.

This skill identifies problems across multiple dimensions: code quality, security, performance, documentation, and architecture.

## Usage

### Analyze a Pull Request

```bash
skill code-review-automation --pr 123
```

### Generate Review Report

```bash
skill code-review-automation --analyze --output review.json
```

### Post Review Comments

```bash
skill code-review-automation --comment --pr 123
```

### CI Integration

```yaml
# GitHub Actions
- name: Code Review Automation
  run: skill code-review-automation --pr ${{ github.event.pull_request.number }}
  env:
    GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

## Review Dimensions

### Code Quality
- Linting violations
- Complexity thresholds
- Naming convention adherence
- Code duplication detection
- Comment quality

### Security
- Dependency vulnerability scanning
- Hardcoded secret detection
- Input validation checks
- Authentication/authorization patterns
- SQL injection prevention

### Tests
- Test coverage thresholds
- Missing test cases
- Test quality assessment
- Flaky test detection

### Documentation
- README updates
- API documentation
- Breaking change notes
- Code comments

### Impact Analysis
- Breaking change detection
- Performance regression risks
- Architecture violations

## Example Output

```
[CODE REVIEW SUMMARY] PR #123

OVERALL: APPROVE WITH CHANGES

CRITICAL: 1
  - src/auth.ts:45 - Hardcoded API key detected

WARNING: 3
  - src/utils/logger.ts:12 - Complex function (cyclomatic: 15)
  - tests/user.test.js: missing edge case for null email
  - src/services/payment.ts - Missing retry logic

INFO: 2
  - Consider extracting validation logic
  - Documentation could include error scenarios

CHANGES REQUIRED: 1
  - Remove hardcoded secret in auth.ts

COVERAGE: 78% (↓ 2% from main)
```

## Configuration

Create `.code-review.yaml`:

```yaml
thresholds:
  max_cyclomatic_complexity: 10
  min_test_coverage: 80
  max_file_lines: 300
  max_function_lines: 30

checks:
  secrets: true
  dependencies: true
  complexity: true
  coverage: true
  documentation: true
  architecture: true

reviewers:
  auto_assign: true
  ownership_file: CODEOWNERS
  fallback: senior-developer

comments:
  post_inline: true
  post_summary: true
```

## Requirements

- OpenCode agent environment
- GitHub/GitLab/Bitbucket access (for PR integration)
- Test coverage tool (for coverage checks)
- Linter configuration file