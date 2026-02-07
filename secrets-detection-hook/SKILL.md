---
name: secrets-detection-hook
description: Block commands and files containing API keys, passwords, or PII before they are committed to version control
license: MIT
compatibility: opencode
metadata:
  audience: developers
  workflow: security
---

## What I do

I prevent sensitive information from being committed to version control by:

- Scanning files for patterns matching API keys, passwords, tokens, and private keys
- Detecting PII such as email addresses, phone numbers, and SSNs in code
- Blocking git commands that would expose secrets
- Providing safe replacement suggestions
- Validating secret rotation and suggesting secure alternatives

## When to use me

Use this skill when:
- You want to prevent secrets from entering the repository
- Setting up pre-commit hooks for a new repository
- Auditing existing codebases for hardcoded credentials
- Validating that secrets have been rotated after a potential exposure

## Usage

This skill runs automatically as a git hook or can be invoked manually:

```bash
skill secrets-detection-hook --scan
```

## Detection Patterns

I scan for:
- AWS Access Keys (AKIA, ABIA, etc.)
- GitHub/GitLab tokens and personal access tokens
- JWT secrets and private keys
- Database connection strings with credentials
- API keys for major services (Stripe, Twilio, SendGrid, etc.)
- Private keys (RSA, EC, DSA)
- Generic password patterns in code
- Email addresses and phone numbers in source files

## Remediation

When a secret is detected, I:
1. Block the operation
2. Explain what was found and why it is dangerous
3. Suggest secure alternatives (environment variables, secret managers)
4. Provide code examples for proper secret handling