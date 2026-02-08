# Documentation Generator

Generate API documentation, code comments, and technical docs from source code.

## Overview

The Documentation Generator skill analyzes source code and produces comprehensive documentation in various formats. It extracts JSDoc/TSDoc comments, generates API reference pages, creates architectural diagrams, and builds complete documentation sites from your codebase.

This skill bridges the gap between code and documentation by keeping them synchronized automatically.

## Usage

### Generate API Documentation

```bash
skill documentation-generator --api
```

### Generate Full Documentation Site

```bash
skill documentation-generator --output docs/
```

### Generate Module Documentation

```bash
skill documentation-generator --module src/auth/
```

### Generate OpenAPI Spec

```bash
skill documentation-generator --openapi --output openapi.json
```

## Output Formats

| Format | Description | Command |
|--------|-------------|---------|
| Markdown | Multi-page docs with navigation | `--output docs/` |
| HTML | Self-hosted documentation site | `--format html` |
| OpenAPI | REST API specification | `--openapi` |
| Docusaurus | React-based docs site | `--format docusaurus` |
| Slate | API reference docs | `--format slate` |

## Documentation Components

### API Reference

Generates documentation for:
- Functions with parameters and return types
- Classes with methods and properties
- Interfaces and type definitions
- Enums and constants
- Module exports

### Code Examples

Extracts examples from:
- Test files (usage patterns)
- Documentation comments
- Sample code blocks
- Integration test scenarios

### Architecture Documentation

Produces:
- Module relationship diagrams
- Component hierarchy charts
- Dependency graphs
- Data flow diagrams

## Example Output

### Input

```typescript
/**
 * Authenticates a user with email and password.
 *
 * @param email - User's email address
 * @param password - User's password
 * @returns Promise resolving to auth token
 *
 * @throws {InvalidCredentialsError} When email/password is invalid
 * @throws {AccountLockedError} When account is locked
 *
 * @example
 * ```ts
 * const token = await authenticate('user@example.com', 'password123');
 * ```
 */
async function authenticate(email: string, password: string): Promise<string> {
  // implementation
}
```

### Generated Markdown

```markdown
## authenticate

```ts
async function authenticate(email: string, password: string): Promise<string>
```

Authenticates a user with email and password.

**Parameters:**

| Name | Type | Description |
|------|------|-------------|
| email | `string` | User's email address |
| password | `string` | User's password |

**Returns:** `Promise<string>` - Promise resolving to auth token

**Throws:**

- `InvalidCredentialsError` - When email/password is invalid
- `AccountLockedError` - When account is locked

**Example:**

```ts
const token = await authenticate('user@example.com', 'password123');
```
```

## Configuration

### Documentation Config

Create `docs.config.json`:

```json
{
  "title": "My API Documentation",
  "version": "1.0.0",
  "format": "markdown",
  "include": ["src/**/*.ts"],
  "exclude": ["src/**/*.test.ts"],
  "plugins": ["docusaurus", "typedoc"],
  "sidebar": {
    "collapsed": false,
    "categories": ["API", "Guides", "Examples"]
  }
}
```

### JSDoc Configuration

```json
// jsdoc.json
{
  "source": {
    "include": ["src"],
    "includePattern": ".+\\.ts$"
  },
  "opts": {
    "outputSourceFiles": true,
    "readme": "README.md"
  }
}
```

## Integration

### With Typedoc

```bash
skill documentation-generator --typedoc --output typedoc/
```

### With Docusaurus

```bash
skill documentation-generator --docusaurus --out docs/
```

### With GitBook

```bash
skill documentation-generator --gitbook --token $GITBOOK_TOKEN
```

## Requirements

- Source files with JSDoc/TSDoc comments
- TypeScript or JavaScript project
- Optional: Typedoc, Docusaurus for enhanced output