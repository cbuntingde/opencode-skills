# Test Generator

Generate comprehensive test suites from source code analysis.

## Overview

The Test Generator skill analyzes source code and automatically produces test suites tailored to your project's testing framework and conventions. It identifies testable units, understands dependencies, and creates meaningful test cases that cover functionality, edge cases, and error handling.

This skill accelerates test development by providing a solid foundation that developers can then refine with domain-specific knowledge and additional scenarios.

## Usage

### Generate Tests for a File

```bash
skill test-generator --file src/utils/parser.ts
```

### Generate Tests for a Directory

```bash
skill test-generator --dir src/services/
```

### Generate Tests with Framework Selection

```bash
# Vitest (default for TypeScript)
skill test-generator --file src/utils.ts --framework vitest

# Jest
skill test-generator --file src/utils.ts --framework jest

# pytest
skill test-generator --file src/utils.py --framework pytest

# JUnit
skill test-generator --file src/Main.java --framework junit
```

### Generate Tests with Coverage Target

```bash
skill test-generator --file src/api.ts --coverage 80
```

## Generated Test Structure

The skill produces tests following the Arrange-Act-Assert pattern:

```typescript
describe('parseUserInput', () => {
  it('should parse valid input successfully', () => {
    const input = { name: 'John', email: 'john@example.com' };
    const result = parseUserInput(input);
    expect(result).toEqual({ name: 'John', email: 'john@example.com' });
  });

  it('should throw error for missing required fields', () => {
    const input = { name: 'John' };
    expect(() => parseUserInput(input)).toThrow(ValidationError);
  });

  it('should trim whitespace from name', () => {
    const input = { name: '  John  ', email: 'john@example.com' };
    const result = parseUserInput(input);
    expect(result.name).toBe('John');
  });
});
```

## Test Types Generated

| Type | Description |
|------|-------------|
| Unit Tests | Test individual functions with mocked dependencies |
| Integration Tests | Test module interactions with real dependencies |
| Edge Case Tests | Boundary values, null/undefined, empty inputs |
| Error Tests | Exception handling, validation failures |

## Configuration

### Framework Detection

The skill automatically detects your testing framework by examining:
- package.json dependencies
- Existing test files
- Configuration files (jest.config.ts, vitest.config.ts, etc.)

### Custom Test Patterns

Add a `.testpatterns.json` file to customize test generation:

```json
{
  "namingConvention": "camelCase",
  "includeDocComments": true,
  "mockExternalCalls": true,
  "testDataGenerators": ["faker", "factory-bot"]
}
```

## Supported Frameworks

| Language | Frameworks |
|----------|------------|
| TypeScript | Vitest, Jest, Mocha |
| JavaScript | Jest, Mocha, Cypress |
| Python | pytest, unittest, nose |
| Java | JUnit 4/5, TestNG |
| Go | testing, Ginkgo, Testify |
| Rust | cargo test, rstest |
| C# | NUnit, xUnit, MSTest |

## Examples

### Basic Function

```typescript
// src/math.ts
export function add(a: number, b: number): number {
  return a + b;
}
```

Generates:

```typescript
// src/math.test.ts
import { add } from './math';

describe('add', () => {
  it('should return sum of two positive numbers', () => {
    expect(add(1, 2)).toBe(3);
  });

  it('should handle negative numbers', () => {
    expect(add(-1, 2)).toBe(1);
  });

  it('should handle zero', () => {
    expect(add(0, 5)).toBe(5);
  });
});
```

### Class with Methods

```typescript
// src/UserService.ts
export class UserService {
  constructor(private db: Database) {}

  async getUser(id: string): Promise<User | null> {
    return this.db.findById(id);
  }

  async createUser(data: CreateUserDto): Promise<User> {
    if (!data.email) throw new Error('Email required');
    return this.db.create(data);
  }
}
```

Generates comprehensive tests including mocks for the Database dependency.

## Requirements

- Source code with clear function signatures
- One of the supported testing frameworks installed
- Write access to test directory