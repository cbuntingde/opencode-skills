# Audit Trail Logger

Capture comprehensive logs of file changes, commands, and decisions for compliance reporting and security investigations.

## Overview

The Audit Trail Logger skill creates detailed, tamper-evident records of all development activities. It provides the documentation needed for regulatory compliance (SOC2, ISO 27001, HIPAA, GDPR), security incident investigations, and change management oversight.

This skill captures every meaningful action during a development session, preserving context, timestamps, and user intent.

## Usage

### Start Recording

```bash
skill audit-trail-logger --start
```

All subsequent activities will be logged to the audit trail.

### Generate Reports

Export the audit trail in various formats:

```bash
# JSON for programmatic processing
skill audit-trail-logger --export audit.json

# HTML for human review
skill audit-trail-logger --report --format html

# CSV for spreadsheet analysis
skill audit-trail-logger --report --format csv
```

### Compliance Reports

Generate reports tailored for specific compliance frameworks:

```bash
# SOC2 compliance report
skill audit-trail-logger --compliance soc2

# ISO 27001 compliance report
skill audit-trail-logger --compliance iso27001

# HIPAA compliance report
skill audit-trail-logger --compliance hipaa
```

## Captured Events

### File Operations
- File creation with content hash
- File modification with before/after diffs
- File deletion with last known content
- Permission and ownership changes

### Git Operations
- Branch creation and deletion
- Commit metadata (author, message, hash)
- Merge and rebase operations
- Tag creation and deletion

### Command Execution
- Command invocation with full arguments
- Execution start/end times
- Exit codes and output summaries
- Working directory context

### Decision Logging
- Explicit user decisions and approvals
- Architecture choices and their rationale
- Trade-off decisions with justification
- Rollback decisions and reasons

### Environment Changes
- Environment variable modifications
- Configuration file changes
- Dependency additions and removals

## Example Output

```json
{
  "timestamp": "2024-01-15T10:30:00Z",
  "event_type": "file_modification",
  "user": "developer@example.com",
  "file": "src/config/auth.js",
  "diff": {
    "before": "const TOKEN_EXPIRY = 3600;",
    "after": "const TOKEN_EXPIRY = 7200;"
  },
  "commit_hash": "abc123",
  "command": "edit src/config/auth.js",
  "rationale": "Increased token expiry to reduce re-authentication friction"
}
```

## Configuration

Configure in `.audit-trail.yaml`:

```yaml
storage:
  location: ./audit-logs
  format: jsonl

retention:
  days: 365
  archive_after: 30

capture:
  file_diff: true
  command_output: summary
  environment_vars: false

compliance:
  framework: auto-detect
  include_rationale: true
```

## Requirements

- OpenCode agent environment
- Write access to audit log directory
- Git repository (for git operation tracking)