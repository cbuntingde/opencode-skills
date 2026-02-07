# Style Mimic

Learn coding patterns and match established conventions automatically.

## Overview

Style Mimic is an OpenCode skill that analyzes existing codebases to identify and extract coding conventions, patterns, and style preferences. It then uses this knowledge to generate new code that seamlessly integrates with the established style of the project.

This skill addresses one of the most challenging aspects of working with unfamiliar codebases: maintaining consistency. When joining a new project or contributing to an existing codebase, developers often struggle to match the existing conventions, leading to style inconsistencies that reduce code quality and readability. Style Mimic solves this by automatically detecting and replicating the patterns used throughout the project.

The skill examines multiple aspects of code style including naming conventions, formatting rules, import organization, error handling approaches, testing strategies, and documentation patterns. It adapts to the specific language, framework, and project preferences, ensuring that generated code feels native to the codebase rather than out of place.

## Usage

The Style Mimic skill is automatically available in OpenCode. To invoke it, simply use the `skill:style-mimic` command followed by your request. The skill will first analyze the relevant portions of your codebase to extract patterns, then apply those patterns when generating code or providing recommendations.

### Prerequisites

- An existing codebase with source files to analyze
- OpenCode installed and configured
- Source files in a supported language (TypeScript, JavaScript, Python, Rust, Go, Java, C#, etc.)

### Invoking the Skill

Use the skill in your conversations with OpenCode:

```
skill:style-mimic Analyze the codebase style conventions
```

Or include specific instructions:

```
skill:style-mimic Create a new API endpoint following existing patterns
```

## Examples

### Analyzing Codebase Conventions

Request a comprehensive analysis of the codebase style:

```
skill:style-mimic
Analyze the entire src/ directory to identify:
- Naming conventions for variables, functions, and classes
- Import organization and structure
- Error handling patterns
- Testing approach and structure
- Commenting and documentation style
```

The skill will examine relevant files and provide a detailed report of the conventions it discovered, which you can use as a reference for future contributions.

### Generating Consistent Code

Generate new code that matches existing style:

```
skill:style-mimic
Create a new utility function called `formatCurrency` that:
- Takes an amount and currency code as parameters
- Returns a formatted string
- Handles null/undefined inputs gracefully
- Matches the existing utility function conventions in src/utils/
```

The skill will analyze similar utility functions in the codebase and generate a new function that follows the same patterns, naming conventions, and error handling approach.

### Learning from Specific Files

Extract patterns from a reference file:

```
skill:style-mimic
Analyze src/services/authService.ts to extract:
- Service layer patterns
- Error handling approach
- Method signatures and naming
- Commenting style

Then generate a new userProfileService.ts following the same conventions.
```

### Matching Component Patterns

Create components that match existing patterns:

```
skill:style-mimic
Analyze the React components in src/components/ to understand:
- Component structure and organization
- Props naming and typing
- Hook usage patterns
- Styling approach

Then generate a new UserAvatar component following these patterns.
```

### Extracting Architectural Patterns

Learn and replicate architectural patterns:

```
skill:style-mimic
Analyze the API route handlers in src/routes/ to identify:
- Request validation patterns
- Response formatting conventions
- Error handling and status codes
- Authentication/authorization patterns

Then generate a new /api/products route handler.
```

## Configuration

Style Mimic requires no additional configuration. It automatically:

- Detects the programming language and applies language-specific conventions
- Identifies framework-specific patterns (React, Express, Django, etc.)
- Adapts to project-specific overrides and preferences
- Respects `.prettierrc`, `.eslintrc`, and other style configuration files
- Learns from the most frequently used patterns in the codebase

If you have specific style guides or conventions documented (e.g., in a STYLEGUIDE.md file), you can reference them in your request and the skill will incorporate those guidelines alongside the automatically detected patterns.

## Requirements

- OpenCode agent framework
- Source code files to analyze (minimum recommended: 5+ relevant files)
- No external dependencies required

The skill works with any programming language and framework. For best results, provide a codebase with sufficient existing code to establish clear patterns (at least 3-5 examples of similar code patterns).