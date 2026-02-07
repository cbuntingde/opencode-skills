---
name: style-mimic
description: Analyze existing codebase patterns and conventions, then generate code that matches the established style
license: MIT
compatibility: opencode
metadata:
  audience: developers
  workflow: code-generation
---

## What I do

- Analyze source files to identify coding conventions, patterns, and style preferences
- Extract naming conventions, formatting rules, code organization patterns
- Generate new code that seamlessly integrates with existing codebase style
- Detect and replicate architectural patterns, error handling approaches, and testing strategies
- Provide recommendations for maintaining consistency across the codebase

## When to use me

Use this skill when:
- Writing new code that must match existing codebase conventions
- Refactoring or extending features in an unfamiliar codebase
- Onboarding to a new project and need to understand its patterns
- Ensuring consistency across contributions from multiple developers
- Creating code templates based on established project patterns

## How I work

1. **Pattern Discovery**: I examine existing code to identify:
   - Naming conventions (camelCase, PascalCase, snake_case)
   - Indentation and formatting preferences
   - Import organization patterns
   - Error handling approaches
   - Testing conventions and frameworks
   - Commenting style and documentation patterns

2. **Style Extraction**: I document the discovered patterns as a reference for code generation

3. **Context-Aware Generation**: I apply the extracted patterns when generating new code

4. **Consistency Validation**: I verify generated code matches the established conventions

## Examples

### Analyzing a codebase

```
skill:style-mimic
Analyze the codebase to identify coding conventions and patterns.
Focus on:
- Naming conventions for variables, functions, and classes
- Import organization and structure
- Error handling patterns
- Testing approach and structure
```

### Generating style-consistent code

```
skill:style-mimic
Create a new utility function for date formatting that matches the existing
codebase conventions. The function should:
- Parse ISO date strings
- Format dates in a user-friendly way
- Handle invalid inputs gracefully
```

### Learning patterns from a specific file

```
skill:style-mimic
Analyze src/utils/logger.ts to extract logging patterns and conventions,
then generate a new metrics collection module following the same approach.
```

## Configuration

This skill automatically detects and adapts to:
- Language-specific conventions (TypeScript, Python, Rust, etc.)
- Framework-specific patterns (React components, API routes, etc.)
- Project-specific overrides and preferences

No additional configuration required.