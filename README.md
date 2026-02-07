# OpenCode Skills Repository

A collection of reusable, AI-powered skills for OpenCode agents that automate complex software development workflows.

## Overview

This repository contains self-contained skill modules that extend OpenCode agent capabilities. Each skill provides a focused set of behaviors for common development tasks, from quality assurance to intent-driven code generation.

Skills in this repository have been designed with production-grade standards, following security best practices, comprehensive error handling, and clean code principles. They adapt to your project's conventions and stack, providing consistent, maintainable results.

## Available Skills

### Intent-to-Code Pipeline

Transforms vague feature requests into production-ready code through a structured five-phase pipeline: intent analysis, architecture design, implementation planning, code generation, and verification.

**Use when:** Requirements are unclear, features are complex, or you need structured guidance from concept to deployment.

```bash
skill intent-to-code
```

[Learn more →](/intent-to-code/README.md)

### QA Analyzer

Performs comprehensive quality assurance checks including code quality assessment, testing coverage verification, security review, performance analysis, and documentation validation.

**Use before:** Releases, deployments, or when ensuring code meets project standards.

```bash
@qa-analyzer Analyze product readiness for this feature
```

[Learn more →](/qa-skill/README.md)

### Style Mimic

Analyzes existing codebases to identify and replicate coding conventions, naming patterns, formatting rules, and architectural approaches when generating new code.

**Use when:** Writing new code in an unfamiliar codebase or maintaining style consistency across contributions.

```bash
skill:style-mimic Create a new utility function following existing patterns
```

[Learn more →](/style-mimic/README.md)

## Quick Start

### Browse Available Skills

Skills are organized in the repository root as self-contained directories. Each skill includes:

- `SKILL.md` - Skill definition with YAML frontmatter and behavioral documentation
- `README.md` - Human-readable documentation with usage examples

### Install a Skill

**Global Installation**
```bash
mkdir -p ~/.config/opencode/skills/
cp -r <skill-name>/ ~/.config/opencode/skills/
```

**Project Installation**
```bash
mkdir -p .opencode/skills/
cp <skill-name>/SKILL.md .opencode/skills/
```

### Using Skills

Once installed, skills are automatically discovered by OpenCode agents. Reference them using the skill tool:

```bash
skill <skill-name>
```

Or invoke through conversation by mentioning the skill name with the `skill:` prefix:

```
skill:style-mimic Analyze the codebase conventions
```

## Skill Structure

All skills follow a consistent structure for easy contribution:

```
skill-name/
├── SKILL.md       # Skill definition (required)
└── README.md      # Documentation (required)
```

### SKILL.md Format

Skills require YAML frontmatter with these fields:

| Field | Required | Description |
|-------|----------|-------------|
| `name` | Yes | Skill identifier (kebab-case, 1-64 chars) |
| `description` | Yes | What the skill does (1-1024 chars) |
| `license` | No | License identifier (e.g., MIT) |
| `compatibility` | No | Compatible platforms |
| `metadata` | No | Additional key-value metadata |

Following the frontmatter, markdown content describes the skill's behavior, use cases, and examples.

### README.md Format

Each skill should include:

- One-line description
- Overview (2-3 paragraphs)
- Usage instructions
- Concrete examples
- Configuration options
- Requirements or prerequisites

## Contributing

Contributions are welcome. To add a new skill:

1. Create a new directory with kebab-case naming
2. Add `SKILL.md` with proper frontmatter
3. Add `README.md` with comprehensive documentation
4. Test the skill with OpenCode
5. Submit a pull request

See [AGENTS.md](/AGENTS.md) for detailed development guidelines.

## Repository Structure

```
opencode-skills/
├── AGENTS.md              # Development guidelines and standards
├── README.md              # This file
├── intent-to-code/        # Multi-phase feature development skill
├── qa-skill/              # Quality assurance analysis skill
└── style-mimic/           # Code pattern matching skill
```

## Requirements

- OpenCode agent framework
- Access to a codebase for implementation tasks
- Compatible with all OpenCode-supported platforms

## License

Individual skills carry their own licenses. See each skill's README for details. The repository structure and documentation are available under the MIT License.

## Topics

ai-agents, automation, developer-tools, opencode, skills