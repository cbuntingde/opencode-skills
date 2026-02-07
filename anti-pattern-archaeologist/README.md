# Anti-Pattern Archaeologist

Detect legacy code smells, anti-patterns, and technical debt in codebases with targeted refactoring recommendations.

## Overview

The Anti-Pattern Archaeologist skill analyzes codebases to identify technical debt, code smells, and anti-patterns that accumulated over time. It provides actionable insights with specific file locations, line numbers, and concrete refactoring suggestions.

This skill is valuable for:
- Understanding the scope of technical debt in legacy systems
- Prioritizing refactoring efforts based on impact and severity
- Building business cases for code modernization
- Onboarding developers to unfamiliar codebases

## Usage

1. Invoke the skill when you need to analyze code quality
2. Specify the scope (entire codebase, specific files, or directories)
3. Review the findings organized by severity and category
4. Apply targeted refactoring recommendations

### Examples

Analyze an entire project:
```
Analyze the codebase for anti-patterns and code smells. Focus on:
- Files in src/
- Test files in tests/
```

Analyze specific patterns:
```
Find all instances of:
- Nested callbacks (callback hell)
- Magic numbers and strings
- Duplicate code blocks
- Functions exceeding 30 lines
- Classes with too many responsibilities
```

Generate refactoring report:
```
Generate a technical debt report for the authentication module:
- Identify all anti-patterns
- Prioritize by severity
- Provide refactoring suggestions with code examples
```

## What I Detect

### Code Smells
- Long methods and functions
- Large classes with too many responsibilities
- Duplicate code blocks
- Magic numbers and hardcoded strings
- Deep nesting (more than 3 levels)
- Long parameter lists
- Feature envy (methods that use more data from other classes)
- Data clumps (groups of variables passed together)
- Speculative generality (unused code for hypothetical future features)
- Refused bequest (subclasses that don't use inherited members)

### Anti-Patterns
- Callback hell (nested asynchronous callbacks)
- God objects (classes with too many responsibilities)
- Circular dependencies
- String concatenation for SQL queries (SQL injection risk)
- Synchronous I/O in request handlers
- Improper error handling (empty catch blocks, swallowing exceptions)
- Mutable shared state
- Shotgun surgery (one change requires editing many files)
- Parallel modification (race conditions)

### Architecture Issues
- Missing input validation
- No authentication/authorization checks
- Insecure cryptographic practices
- Missing rate limiting
- Missing security headers
- Hardcoded secrets and credentials
- Incomplete error handling

### Output Format

Each finding includes:
- **Category**: Type of anti-pattern or code smell
- **Severity**: Critical, High, Medium, Low, Informational
- **Location**: File path and line number
- **Description**: What the issue is
- **Impact**: Why this matters
- **Recommendation**: Specific refactoring steps
- **Before/After**: Code comparison showing the fix

## Configuration

No configuration required. The skill automatically:
- Detects programming language from file extensions
- Applies language-specific patterns and rules
- Skips vendored code and dependencies
- Ignores test files unless explicitly requested

## Requirements

- Access to the codebase files to analyze
- No external dependencies or APIs required
- Works with any programming language (TypeScript/JavaScript, Python, Go, Rust, Java, C/C++, etc.)