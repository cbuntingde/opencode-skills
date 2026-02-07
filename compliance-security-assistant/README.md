# Compliance & Security Assistant

Scan codebases for GDPR, HIPAA, SOC2 violations and validate PII handling practices.

## Overview

The Compliance & Security Assistant skill helps developers and security teams identify regulatory compliance violations in code. It analyzes source code, configuration files, and data flow patterns to detect potential violations of major compliance frameworks.

This skill is designed for organizations handling sensitive data who need to ensure their codebase meets regulatory requirements before deployment.

## Usage

### Quick Scan

```bash
skill compliance-security-assistant --scan
```

### Framework-Specific Report

```bash
# GDPR compliance report
skill compliance-security-assistant --report --framework gdpr

# HIPAA compliance report
skill compliance-security-assistant --report --framework hipaa

# SOC2 compliance report
skill compliance-security-assistant --report --framework soc2
```

### Strict Validation

Enable strict mode for more aggressive checking:

```bash
skill compliance-security-assistant --validate --strict
```

### CI Integration

```yaml
# GitHub Actions
- name: Compliance Scan
  run: skill compliance-security-assistant --scan --fail-on violations
```

## Detected Issues

### GDPR Violations

| Issue | Severity | Example |
|-------|----------|---------|
| User email stored without consent check | High | Database field without consent tracking |
| Missing data deletion endpoint | Medium | No DELETE /user/{id} endpoint |
| Data retention not implemented | Medium | No TTL on user data |
| Missing data portability endpoint | Low | No GET /user/export endpoint |

### HIPAA Violations

| Issue | Severity | Example |
|-------|----------|---------|
| PHI logged without masking | Critical | console.log(patientRecord) |
| Missing access logging | High | No audit trail for PHI access |
| Unencrypted PHI storage | Critical | Base64 encoded SSN in database |
| No session timeout | Medium | Infinite session duration |

### SOC2 Violations

| Issue | Severity | Example |
|-------|----------|---------|
| Missing rate limiting | High | No throttling on auth endpoints |
| Inadequate password policy | Medium | No minimum password length |
| Missing security headers | Low | No X-Content-Type-Options header |
| No failed login tracking | Medium | No lockout mechanism |

## Example Output

```
[COMPLIANCE SCAN RESULTS]
Framework: GDPR
Timestamp: 2024-01-15T10:30:00Z

VIOLATIONS FOUND: 3

1. HIGH: Email stored without consent tracking
   File: src/models/User.js:42
   Recommendation: Add consent_date field and validate before storage

2. MEDIUM: No data deletion implementation
   File: src/routes/user.js
   Recommendation: Implement DELETE /api/users/:id endpoint

3. LOW: Data retention policy not documented
   File: docs/data-retention.md:missing
   Recommendation: Document data retention periods
```

## Configuration

Create `.compliance-config.yaml`:

```yaml
frameworks:
  gdpr:
    enabled: true
    strict_mode: false
  hipaa:
    enabled: true
    strict_mode: true
  soc2:
    enabled: true

scan:
  include:
    - "**/*.js"
    - "**/*.ts"
    - "**/*.py"
  exclude:
    - "**/test/**"
    - "**/node_modules/**"

severity_levels:
  critical: fail-immediately
  high: fail-before-merge
  medium: warning
  low: info
```

## Requirements

- OpenCode agent environment
- Access to source code directory