# Secrets Detection Hook

Prevent hardcoded secrets, API keys, and PII from being committed to version control.

## Overview

The Secrets Detection Hook skill proactively prevents sensitive information from entering your repository. It scans files for hardcoded credentials, API keys, passwords, and personally identifiable information (PII) before they can be committed, blocking potentially costly security incidents.

This skill uses pattern matching and entropy analysis to detect a wide variety of secret formats, from obvious hardcoded passwords to subtle high-entropy strings that may be API keys.

## Usage

### Automatic Hook

Configure as a pre-commit hook to automatically scan files before each commit:

```bash
# Install as pre-commit hook
skill secrets-detection-hook --install-hook
```

### Manual Scan

Scan a specific file or directory:

```bash
skill secrets-detection-hook --scan src/config/
```

### CI Integration

Run in CI pipelines to catch secrets in pull requests:

```yaml
# GitHub Actions example
- name: Secrets Detection
  run: skill secrets-detection-hook --ci
```

## Detected Patterns

### Credentials & Keys
- AWS Access Key IDs and Secret Keys
- GitHub/GitLab/Bitbucket tokens
- Stripe API keys (sk_live, pk_live)
- Twilio, SendGrid, and other service API keys
- JWT secrets and signing keys
- RSA, EC, and DSA private keys
- Database connection strings with embedded credentials

### PII
- Email addresses in source files
- Phone numbers
- Social Security Number patterns
- Credit card numbers

### Generic Secrets
- Password assignment patterns
- Environment variable assignments with values
- Configuration files containing secrets

## Examples

**Blocked commit attempt:**
```
$ git commit -m "add config"
[SECRETS DETECTED] Blocking commit

Found: AWS Access Key in config.py:15
Pattern: AKIA2ABCDEFGHIJKLMNO
Severity: CRITICAL

Recommendation: Use environment variables or AWS Secrets Manager
```

**Safe alternative:**
```python
# Instead of hardcoded credentials
AWS_ACCESS_KEY = "AKIA2ABCDEFGHIJKLMNO"  # BLOCKED

# Use environment variables
import os
AWS_ACCESS_KEY = os.environ.get("AWS_AWS_ACCESS_KEY")  # SAFE
```

## Configuration

Create a `.secrets-detection.yaml` configuration:

```yaml
patterns:
  custom:
    - name: Company API Key
      pattern: "company_[a-zA-Z0-9]{32}"
      severity: high

ignore:
  - "**/test/**"
  - "**/__pycache__/**"

entropy:
  threshold: 4.5
  min_length: 16
```

## Requirements

- OpenCode agent environment
- Python 3.8+ (for regex and pattern matching)
- Optional: pre-commit framework for hook integration