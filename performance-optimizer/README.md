# Performance Optimizer

Identify performance bottlenecks and apply optimizations to code.

## Overview

The Performance Optimizer skill analyzes code to find and fix performance issues. It examines database queries, memory usage, CPU utilization, and algorithmic complexity to recommend and implement improvements. The skill provides actionable recommendations with quantified impact estimates.

This skill helps maintain responsive applications by catching performance issues before they affect users.

## Usage

### Analyze Code for Bottlenecks

```bash
skill performance-optimizer --analyze src/api/
```

### Profile Critical Path

```bash
skill performance-optimizer --profile /api/users/:id
```

### Generate Optimization Report

```bash
skill performance-optimizer --report --output perf-report.md
```

### Apply Recommended Fixes

```bash
skill performance-optimizer --apply --dry-run
```

## Detected Issues

### Database

| Issue | Impact | Detection |
|-------|--------|-----------|
| N+1 queries | High | Loading related entities in loops |
| Missing indexes | High | Slow queries on large tables |
| Unnecessary selects | Medium | Fetching unused columns |
| Batch operations | Medium | Individual inserts/updates |

### Memory

| Issue | Impact | Detection |
|-------|--------|-----------|
| Memory leaks | High | Growing heap over time |
| Large objects | Medium | Loading excessive data |
| Caching missing | Medium | Repeated computations |
| Closure captures | Low | Unnecessary object retention |

### Algorithm

| Issue | Impact | Detection |
|-------|--------|-----------|
| O(n²) or worse | High | Nested loops on large data |
| Unnecessary work | Medium | Redundant iterations |
| Early termination | Low | Missing break/return |
| Memoization | Low | Repeated pure function calls |

## Example Optimization

### Before (N+1 Query)

```typescript
const users = await db.findAll('users');
for (const user of users) {
  const posts = await db.find('posts', { userId: user.id }); // Query per user
}
```

### After (Eager Load)

```typescript
const users = await db.findAll('users', { include: 'posts' });
// Single query with JOIN, no N+1
```

### Before (Unoptimized)

```typescript
function findDuplicates(items: string[]): string[] {
  const duplicates: string[] = [];
  for (let i = 0; i < items.length; i++) {
    for (let j = 0; j < items.length; j++) { // O(n²)
      if (i !== j && items[i] === items[j]) {
        duplicates.push(items[i]);
      }
    }
  }
  return [...new Set(duplicates)];
}
```

### After (Optimized)

```typescript
function findDuplicates(items: string[]): string[] {
  const seen = new Set<string>();
  const duplicates = new Set<string>();
  for (const item of items) {
    if (seen.has(item)) {
      duplicates.add(item);
    } else {
      seen.add(item);
    }
  }
  return Array.from(duplicates);
}
```

## Configuration

### Optimization Profile

```json
{
  "focus": ["database", "memory"],
  "threshold": {
    "slowQueryMs": 100,
    "memoryGrowthMb": 50
  },
  "includeTests": false,
  "autoApply": false
}
```

### Caching Recommendations

```json
{
  "cache": {
    "ttl": 300,
    "strategy": "lru",
    "maxSize": 1000
  }
}
```

## Metrics Tracked

| Metric | Target | Warning |
|--------|--------|---------|
| Query time | < 50ms | > 100ms |
| Memory growth | < 10MB/min | > 50MB/min |
| API response | < 200ms | > 500ms |
| Bundle size | < 500KB | > 1MB |

## Requirements

- Source code access for analysis
- Database query logs (optional for query analysis)
- Performance test suite (recommended)