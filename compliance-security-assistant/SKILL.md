---
name: compliance-security-assistant
description: Scan code for GDPR, HIPAA, SOC2 violations, and validate PII handling practices
license: MIT
compatibility: opencode
metadata:
  audience: security-engineers
  workflow: compliance
---

## What I do

I identify compliance violations by:

- Scanning for GDPR, HIPAA, and SOC2 policy violations
- Detecting improper PII handling in code
- Validating data retention compliance
- Checking consent management implementation
- Verifying encryption requirements
- Generating compliance remediation reports

## When to use me

Use this skill when:
- Preparing for compliance audits
- Building applications that handle sensitive data
- Reviewing third-party code for compliance
- Validating data handling practices
- Creating compliance documentation

## Usage

```bash
skill compliance-security-assistant --scan
skill compliance-security-assistant --report --framework gdpr
skill compliance-security-assistant --validate --strict
```

## Checked Compliance Areas

### GDPR
- Data minimization
- Right to erasure implementation
- Consent management
- Data portability
- Purpose limitation

### HIPAA
- PHI access controls
- Encryption at rest and in transit
- Audit logging
- Breach notification logic

### SOC2
- Access control implementation
- Change management
- Risk assessment
- Security monitoring