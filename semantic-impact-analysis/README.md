# Semantic Impact Analysis

Understand the ripple effects of code changes before you make them.

## Overview

Semantic Impact Analysis is a skill that helps developers understand the full consequences of code modifications. When you need to change a function, refactor a module, or update an API, this skill traces dependencies, identifies affected tests, and predicts potential breaking changes.

Rather than discovering bugs after deployment, use this skill proactively to map out the blast radius of your changes. It's essential for safe refactoring, deprecation planning, and understanding legacy codebases.

## Usage

### Prerequisites

- An OpenCode-compatible project with accessible source code
- No additional dependencies required

### Invoking the skill

Describe what you want to change and why. The skill will analyze the codebase and provide:

1. **Direct dependencies**: What code immediately depends on the change
2. **Transitive impact**: How effects cascade through the system
3. **Test coverage**: Which tests validate affected functionality
4. **Risk assessment**: Severity and scope of potential issues
5. **Recommendations**: Safe migration strategies when possible

### Example queries

- "What breaks if I rename the `calculateTotal` function in the billing module?"
- "I'm removing the deprecated email service—what consumers need updates?"
- "Show me all tests that would catch bugs in the user authentication flow"
- "What is the impact of changing the API response shape of the `/users` endpoint?"
- "Find all places that depend on the current configuration schema"

## How it works

The skill uses static analysis techniques to trace relationships in your codebase:

- **Import analysis**: Map module dependencies
- **Call graph construction**: Find function callers and callees
- **Type dependency tracing**: Identify type consumers
- **Test mapping**: Link tests to code they exercise
- **Contract analysis**: Review public API usage patterns

## Output format

When you request an impact analysis, you receive:

- **Summary**: One-sentence risk assessment
- **Affected files**: Categorized by impact level (high, medium, low)
- **Test coverage**: Tests that would catch regressions
- **Migration guidance**: Step-by-step plans for safe changes
- **Open questions**: Areas requiring manual review

## Best practices

Use this skill before:

- Making breaking changes to public APIs
- Refactoring shared utilities or base classes
- Changing data schemas or interfaces
- Removing deprecated code
- Modifying configuration formats
- Any change that affects multiple modules

## Common patterns

The skill recognizes common impact scenarios:

- **Shared utility changes**: Affect all consumers
- **Configuration schema changes**: Affect all config readers
- **Interface modifications**: Break implementing classes
- **Event/hook changes**: Affect all publishers/consumers
- **Database schema changes**: Affect ORMs, queries, and migrations

## Limitations

- Cannot detect runtime behavioral changes that don't appear in static analysis
- Cannot predict business logic impacts without domain knowledge
- Cannot access external API consumers outside the codebase
- Analysis depth depends on project size and complexity