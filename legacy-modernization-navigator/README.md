# Legacy Modernization Navigator

Analyze legacy tech stacks and create incremental migration strategies with phased modernization roadmaps.

## Overview

The Legacy Modernization Navigator skill provides comprehensive analysis of existing technology stacks and generates actionable migration plans. Instead of risky big-bang rewrites, it recommends incremental modernization strategies that allow teams to modernize gradually while maintaining business continuity.

This skill is essential for:
- Organizations with long-lived codebases accumulated over decades
- Teams facing end-of-life dependencies that need urgent replacement
- Projects requiring technology upgrades with minimal disruption
- Enterprises needing to justify modernization investments to stakeholders
- Teams seeking to adopt modern development practices without complete rewrites

## Usage

1. Invoke the skill to analyze the current technology landscape
2. Review the inventory of dependencies, versions, and their status
3. Receive a prioritized migration roadmap with phases
4. Get specific recommendations for each component
5. Implement changes incrementally with provided checkpoints

### Examples

Analyze a full technology stack:
```
Analyze the technology stack for this project:
- Identify all dependencies and their versions
- Flag deprecated or end-of-life technologies
- Assess security vulnerabilities in dependencies
- Create a migration roadmap for the next 12 months
```

Focus on specific concerns:
```
Analyze the frontend technology stack:
- Check for deprecated React patterns
- Identify outdated CSS approaches
- Recommend modern alternatives to legacy build tools
```

Plan a migration:
```
Create an incremental migration plan for moving from AngularJS to React:
- Identify components that can be migrated incrementally
- Recommend shared component libraries
- Plan for parallel running of both frameworks
- Define integration points and data flow between frameworks
```

## What I Analyze

### Technology Inventory
- Programming languages and versions
- Frameworks and their versions
- Package managers and build tools
- Database systems and ORMs
- Message queues and caching layers
- Cloud services and infrastructure
- Testing frameworks and CI/CD tools
- Monitoring and observability tools

### Risk Assessment
- Dependencies at end-of-life or approaching EOL
- Security vulnerabilities by severity
- Deprecated APIs and breaking changes ahead
- Technical debt accumulated over time
- Dependency complexity and relationships
- License compliance issues

### Migration Recommendations
- Modern alternatives with feature comparisons
- Migration complexity estimates
- Breaking change impact analysis
- Compatibility layers and shims
- Parallel running strategies
- Rollback procedures

## Output Format

### Dependency Report
Each dependency includes:
- Current version and release date
- Latest stable version
- End-of-life date if applicable
- Known security vulnerabilities
- Recommended upgrade path
- Complexity level for migration

### Migration Roadmap
Organized by phases:
- **Phase 1 (Immediate)**: Critical security and stability fixes
- **Phase 2 (Short-term)**: Low-risk dependency updates
- **Phase 3 (Medium-term)**: Feature upgrades and moderate refactoring
- **Phase 4 (Long-term)**: Architecture changes and technology replacement

Each phase includes:
- List of changes with justification
- Estimated effort (story points or developer days)
- Risk level and mitigation strategies
- Success criteria and checkpoints
- Rollback procedures

### Decision Matrix
When multiple migration paths exist, I provide:
- Comparison of options with pros/cons
- Total cost of ownership analysis
- Long-term maintenance considerations
- Team skill alignment recommendations
- Ecosystem maturity comparison

## Configuration

The skill automatically:
- Detects project type from file patterns
- Identifies dependency files (package.json, pom.xml, go.mod, etc.)
- Skips node_modules, vendored code, and build artifacts
- Respects .gitignore patterns for analysis scope
- Adapts recommendations based on project size

No configuration required. All settings are inferred from the codebase structure.

## Requirements

- Access to project files and configuration
- No external API calls or network dependencies
- Works with any programming language and framework
- Compatible with monorepo and polyrepo structures