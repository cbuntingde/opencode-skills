---
name: cost-monitor-hook
description: Track and alert on expensive cloud operations, API calls, and resource usage to prevent unexpected bills
license: MIT
compatibility: opencode
metadata:
  audience: devops
  workflow: cost-management
---

## What I do

I track costs by:

- Monitoring API calls to expensive services
- Detecting resource-intensive operations
- Alerting before costly operations execute
- Tracking cloud resource provisioning
- Summarizing session costs
- Suggesting cost optimization opportunities

## When to use me

Use this skill when:
- Working with paid APIs (OpenAI, AWS, cloud services)
- Provisioning cloud resources
- Running batch operations on metered services
- Optimizing cloud costs
- Setting budget alerts

## Usage

```bash
skill cost-monitor-hook --track
skill cost-monitor-hook --alert --threshold 10
skill cost-monitor-hook --report
```

## Tracked Costs

I monitor:
- Cloud API calls (AWS, GCP, Azure)
- Database query costs
- External service calls
- Compute resource provisioning
- Storage operations