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

---

# OpenCode Plugins

Plugins extend OpenCode with custom code (JavaScript/TypeScript). Unlike skills which provide behavioral instructions, plugins can hook into events, modify execution, and add custom tools.

## Plugin Locations

- **Project-level**: `.opencode/plugins/`
- **Global**: `~/.config/opencode/plugins/`
- **NPM packages**: Add to `plugin` array in `opencode.json`

Example `opencode.json`:
```json
{
  "plugin": ["opencode-wakatime", "@my-org/custom-plugin"]
}
```

## Plugin Structure

A plugin is a JavaScript/TypeScript module that exports a function returning hooks:

```javascript
// .opencode/plugins/my-plugin.js
export const MyPlugin = async ({ project, client, $, directory, worktree }) => {
  return {
    "tool.execute.before": async (input, output) => {
      // Modify tool execution
    },
  };
};
```

### Context Properties

- `project` - Current project information
- `client` - OpenCode SDK client for AI interaction
- `$` - Bun shell API for executing commands
- `directory` - Current working directory
- `worktree` - Git worktree path

## TypeScript Support

Import types from `@opencode-ai/plugin`:

```typescript
import type { Plugin } from "@opencode-ai/plugin";

export const MyPlugin: Plugin = async (ctx) => {
  return {
    // Type-safe hook implementations
  };
};
```

## External Dependencies

Add `package.json` to your config directory for npm dependencies:

```json
// .opencode/package.json
{
  "dependencies": {
    "shescape": "^2.1.0"
  }
}
```

OpenCode runs `bun install` at startup. Import in plugins:

```javascript
import { escape } from "shescape";
```

## Available Events

### Command Events
- `command.executed`

### File Events
- `file.edited`
- `file.watcher.updated`

### Tool Events
- `tool.execute.before`
- `tool.execute.after`

### Shell Events
- `shell.env`

### Session Events
- `session.created`
- `session.compacted`
- `session.deleted`
- `session.idle`
- `session.status`

### Message Events
- `message.updated`
- `message.removed`

### LSP Events
- `lsp.client.diagnostics`
- `lsp.updated`

### Permission Events
- `permission.asked`
- `permission.replied`

## Custom Tools

Plugins can add custom tools:

```typescript
import { type Plugin, tool } from "@opencode-ai/plugin";

export const CustomToolsPlugin: Plugin = async (ctx) => {
  return {
    tool: {
      mytool: tool({
        description: "This is a custom tool",
        args: {
          foo: tool.schema.string(),
        },
        async execute(args, context) {
          return `Hello ${args.foo}`;
        },
      }),
    },
  };
};
```

## Examples

### Prevent .env access
```javascript
export const EnvProtection = async () => {
  return {
    "tool.execute.before": async (input, output) => {
      if (input.tool === "read" && output.args.filePath.includes(".env")) {
        throw new Error("Do not read .env files");
      }
    },
  };
};
```

### Inject environment variables
```javascript
export const InjectEnvPlugin = async () => {
  return {
    "shell.env": async (input, output) => {
      output.env.MY_API_KEY = "secret";
    },
  };
};
```

### Send notifications
```javascript
export const NotificationPlugin = async ({ $ }) => {
  return {
    event: async ({ event }) => {
      if (event.type === "session.idle") {
        await $`osascript -e 'display notification "Session done!"'`;
      }
    },
  };
};
```

## Logging

Use `client.app.log()` for structured logging:

```javascript
export const MyPlugin = async ({ client }) => {
  await client.app.log({
    body: {
      service: "my-plugin",
      level: "info",
      message: "Plugin initialized",
    },
  });
};
```

Levels: `debug`, `info`, `warn`, `error`.

## Load Order

1. Global config (`~/.config/opencode/opencode.json`)
2. Project config (`opencode.json`)
3. Global plugin directory (`~/.config/opencode/plugins/`)
4. Project plugin directory (`.opencode/plugins/`)

Duplicate npm packages load once. Local and npm plugins with similar names load separately.