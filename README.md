# OpenCode Skills Repository

A collection of reusable, AI-powered skills for OpenCode agents that automate complex software development workflows.

## Overview

Self-contained skill modules that extend OpenCode agent capabilities. Each skill provides focused behaviors for common development tasks—quality assurance, code analysis, security, compliance, and more. Skills adapt to your project's conventions and stack.

## Skills by Category

### Code Quality & Analysis
| Skill | Description |
|-------|-------------|
| [Codebase Cartographer](/codebase-cartographer/README.md) | Visualize architectural boundaries and dependency relationships |
| [Style Mimic](/style-mimic/README.md) | Learn coding patterns and match established conventions |
| [Anti-Pattern Archaeologist](/anti-pattern-archaeologist/README.md) | Detect legacy code smells, anti-patterns, and technical debt |
| [Semantic Impact Analysis](/semantic-impact-analysis/README.md) | Understand ripple effects of code changes before making them |

### Architecture & Standards
| Skill | Description |
|-------|-------------|
| [Architecture Gatekeeper](/architecture-gatekeeper/README.md) | Prevent commits violating architecture patterns or circular dependencies |
| [Code Policy Enforcer](/code-policy-enforcer/README.md) | Enforce team coding standards and forbidden patterns |
| [Code Review Automation](/code-review-automation/README.md) | Automate code review workflows and PR analysis |

### Testing & CI/CD
| Skill | Description |
|-------|-------------|
| [Test Generator](/test-generator/README.md) | Generate comprehensive test suites from source code |
| [QA Analyzer](/qa-skill/README.md) | Comprehensive QA checks for releases and deployments |
| [CI/CD Healer](/ci-cd-healer/README.md) | Diagnose and fix flaky tests, optimize pipeline caching |

### Performance & Maintenance
| Skill | Description |
|-------|-------------|
| [Performance Optimizer](/performance-optimizer/README.md) | Identify bottlenecks and apply code optimizations |
| [Dependency Upgrader](/dependency-upgrader/README.md) | Safely upgrade dependencies and manage breaking changes |

### Documentation
| Skill | Description |
|-------|-------------|
| [Documentation Generator](/documentation-generator/README.md) | Generate API docs, comments, and technical documentation |

### Security & Compliance
| Skill | Description |
|-------|-------------|
| [Compliance & Security Assistant](/compliance-security-assistant/README.md) | Scan for GDPR, HIPAA, SOC2 violations and PII handling |
| [Secrets Detection Hook](/secrets-detection-hook/README.md) | Prevent hardcoded secrets and PII from being committed |
| [Audit Trail Logger](/audit-trail-logger/README.md) | Capture comprehensive logs for compliance and security |

### Safety & Operations
| Skill | Description |
|-------|-------------|
| [Environment Guard](/environment-guard/README.md) | Block dangerous operations in production |
| [Cost Monitor Hook](/cost-monitor-hook/README.md) | Track and alert on expensive cloud operations |
| [Legacy Modernization Navigator](/legacy-modernization-navigator/README.md) | Analyze legacy stacks and create incremental migration plans |

### Development Workflow
| Skill | Description |
|-------|-------------|
| [Intent-to-Code Pipeline](/intent-to-code/README.md) | Multi-step feature generation from concept to code |

## Quick Start

**Install a skill globally:**
```bash
mkdir -p ~/.config/opencode/skills/
cp -r <skill-name>/ ~/.config/opencode/skills/
```

**Install in project:**
```bash
mkdir -p .opencode/skills/
cp <skill-name>/SKILL.md .opencode/skills/
```

**Use a skill:**
```bash
skill <skill-name>
# or
@skill-name Your request here
```

## Structure

```
skill-name/
├── SKILL.md       # Skill definition with YAML frontmatter
└── README.md      # Human-readable documentation
```

See [AGENTS.md](/AGENTS.md) for development guidelines.

## License

Individual skills carry their own licenses. Repository structure and documentation are MIT licensed.