# QA Analyzer Skill

A comprehensive QA analysis skill for OpenCode that performs product readiness evaluations.

## Overview

This skill provides automated quality assurance checks for software products before release. It evaluates code quality, testing coverage, security, performance, documentation, and deployment readiness.

## Installation

### Global Installation
```bash
cp -r qa-skill ~/.config/opencode/agents/
```

### Project Installation
```bash
mkdir -p .opencode/agents
cp qa-analyzer.md .opencode/agents/
```

## Usage

Invoke the skill using OpenCode:

```
@qa-analyzer Analyze product readiness for this feature
@qa-analyzer Check code quality and testing coverage
@qa-analyzer Perform security audit before release
```

## What It Checks

### Code Quality
- Coding conventions and style consistency
- Error handling implementation
- Code readability and maintainability
- Proper commenting and documentation

### Testing Coverage
- Unit test existence and quality
- Integration test coverage
- Edge case testing
- Test suite execution status
- Coverage threshold validation

### Security
- Hardcoded secrets detection
- Input validation
- Authentication/authorization
- SQL injection prevention
- XSS and CSRF protection
- Dependency vulnerability scanning

### Performance
- N+1 query pattern detection
- Database query optimization
- API response times
- Memory usage efficiency
- Caching implementation

### Documentation
- README accuracy and completeness
- API documentation
- Setup instructions
- Architecture decision records

### Build & Deployment
- Build process validation
- Dependency management
- Environment configuration
- Migration and rollback procedures

## Output Format

The analyzer provides:

1. **Summary Table** - Pass/Warn/Fail status per category
2. **Detailed Findings** - Each issue with:
   - Severity level (Critical/High/Medium/Low)
   - Category and description
   - File location and line number
   - Fix recommendations
3. **Overall Assessment** - Ready for release verdict with next steps

## Project Structure

```
qa-skill/
├── README.md                 # This file
├── qa-analyzer.md            # Skill definition file
└── prompts/
    └── qa-checklist.txt      # QA checklist prompts
```

## Requirements

- OpenCode CLI tool
- Bash access for file exploration
- Read permissions for codebase analysis

## License

MIT