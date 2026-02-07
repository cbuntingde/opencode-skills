---
name: audit-trail-logger
description: Capture all file changes, commands, and decisions for compliance reporting and audit purposes
license: MIT
compatibility: opencode
metadata:
  audience: security-engineers
  workflow: compliance
---

## What I do

I create comprehensive audit trails by:

- Tracking all file modifications with diff capture
- Recording commands executed during sessions
- Logging decisions and their rationale
- Generating compliance reports for regulatory requirements
- Preserving evidence for security incident investigations
- Timestamping all entries with timezone information

## When to use me

Use this skill when:
- Preparing for security audits (SOC2, ISO 27001, HIPAA)
- Investigating security incidents
- Documenting change approval workflows
- Meeting regulatory compliance requirements
- Creating paper trails for critical operations

## Usage

```bash
skill audit-trail-logger --start
skill audit-trail-logger --export
skill audit-trail-logger --report --format html
```

## Captured Data

I capture:
- File creation, modification, and deletion events
- Git operations (commits, merges, branches)
- Command executions and their outputs
- User decisions and approvals
- Environment changes and configuration modifications
- API calls to external services