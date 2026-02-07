---
name: semantic-impact-analysis
description: Analyze code changes to understand potential ripple effects, identify affected dependencies, and predict what functionality might break
license: MIT
compatibility: opencode
metadata:
  audience: developers
  workflow: all
  domain: code-analysis
---

## What I do

I help you understand the consequences of code changes before you make them. I analyze:

- **Dependency chains**: What modules, functions, and components depend on the code you're changing
- **Test coverage**: Which tests validate the functionality that might be affected
- **API contracts**: What interfaces, exports, or contracts might be impacted
- **Side effects**: Behavioral changes that could propagate through the system
- **Migration paths**: How to safely refactor or deprecate functionality

## When to use me

Use me when you need to:

- Understand risks before refactoring a module
- Plan a safe migration or deprecation
- Identify all tests that need to pass after a change
- Find hidden dependencies on a function or class
- Understand the blast radius of a breaking change
- Review a pull request for potential issues

## How I work

I systematically analyze code changes through:

1. **Static analysis**: Trace imports, exports, and type dependencies
2. **Call graph traversal**: Find all callers and callees of changed functions
3. **Test discovery**: Identify tests that exercise changed code paths
4. **Contract analysis**: Review API boundaries and integration points
5. **Pattern detection**: Recognize common impact patterns (e.g., configuration coupling, shared state)

## Commands

Start an impact analysis by describing what you want to change:

```
I want to change the UserService.getUser method to return a different shape
```

```
I'm planning to remove the legacy auth module
```

```
Help me understand what breaks if I change this config format
```

```
What tests should I run after modifying the payment gateway?
```

## Analysis scope

I can analyze impact across:

- **Single file changes**: Understand local and downstream effects
- **Module refactoring**: Identify all consumers of internal APIs
- **Public API changes**: Trace all external consumers
- **Schema changes**: Find code that depends on data structures
- **Configuration changes**: Identify code that reads or generates config