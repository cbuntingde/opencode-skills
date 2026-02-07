# OpenCode Skills Repository

This repository contains OpenCode agent skills. Each skill is a self-contained module that provides reusable behavior for OpenCode agents.

## Project Structure

- `/` - Root directory containing skill directories
- Each skill has its own directory named with kebab-case (e.g., `git-release`, `code-review`)
- Each skill directory contains a `SKILL.md` file with the skill definition

## Skill Structure

Each skill must be in its own directory with the following structure:

```
skill-name/
├── SKILL.md
└── README.md
```

### SKILL.md (Required)
The skill definition file containing YAML frontmatter and behavioral documentation.

### README.md (Required)
A professional README providing human-readable documentation for skill users:

```
# Skill Name

Brief one-line description

## Overview

2-3 paragraph overview of what the skill does and when to use it

## Usage

Prerequisites, setup steps, and how to invoke the skill

## Examples

Concrete examples demonstrating common use cases

## Configuration

Any configurable options or parameters

## Requirements

Prerequisites, dependencies, or compatible platforms
```

Write in clear, professional markdown with:
- Consistent heading hierarchy
- Code blocks with language annotations
- Bulleted and numbered lists where appropriate
- Links to related skills or resources

### SKILL.md Format

Every `SKILL.md` must include YAML frontmatter with:

- `name` (required) - Skill identifier, 1-64 characters, lowercase alphanumeric with single hyphens
- `description` (required) - What the skill does, 1-1024 characters
- `license` (optional) - License for the skill
- `compatibility` (optional) - Compatible platforms (e.g., "opencode")
- `metadata` (optional) - Additional metadata as key-value pairs

The frontmatter is followed by markdown content describing the skill.

Example:

```yaml
---
name: git-release
description: Create consistent releases and changelogs
license: MIT
compatibility: opencode
metadata:
  audience: maintainers
  workflow: github
---

## What I do
- Draft release notes from merged PRs
- Propose a version bump
- Provide a copy-pasteable `gh release create` command

## When to use me
Use this when you are preparing a tagged release.
```

## Naming Conventions

Skill names must:
- Be 1-64 characters
- Be lowercase alphanumeric with single hyphen separators
- Not start or end with `-`
- Not contain consecutive `--`
- Match the directory name

Pattern: `^[a-z0-9]+(-[a-z0-9]+)*$`

## Skill Discovery Locations

Skills are discovered from these locations:
- Project: `.opencode/skills/<name>/SKILL.md`
- Global: `~/.config/opencode/skills/<name>/SKILL.md`
- Claude-compatible Project: `.claude/skills/<name>/SKILL.md`
- Claude-compatible Global: `~/.claude/skills/<name>/SKILL.md`
- Agent-compatible Project: `.agents/skills/<name>/SKILL.md`
- Agent-compatible Global: `~/.agents/skills/<name>/SKILL.md`

## Development Guidelines

When creating or modifying skills:

1. Create a new directory for each skill using kebab-case
2. Use `SKILL.md` (all caps) for the skill definition file
3. Include both `name` and `description` in frontmatter
4. Keep descriptions specific enough for agents to choose correctly
5. Write clear documentation in the skill body
6. Create a professional `README.md` for human users
7. Test skills by loading them in OpenCode

## Quality Standards

- Each skill should have a focused, single purpose
- Descriptions should clearly state when to use the skill
- Include examples or usage instructions where helpful
- Skills should be self-contained and not depend on external resources
- Update skill descriptions when functionality changes

## Permission Configuration

Skills can be controlled via permissions in `opencode.json`:

```json
{
  "permission": {
    "skill": {
      "*": "allow",
      "pr-review": "allow",
      "internal-*": "deny",
      "experimental-*": "ask"
    }
  }
}
```

- `allow` - Skill loads immediately
- `deny` - Skill hidden from agent
- `ask` - User prompted before loading

## Testing Skills

To test a new skill:
1. Ensure the skill is in the correct directory structure
2. Start OpenCode in the repository
3. Use the `/init` command to refresh skill discovery
4. Invoke the skill using the native `skill` tool