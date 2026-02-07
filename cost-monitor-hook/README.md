# Cost Monitor Hook

Track and alert on expensive cloud operations, API calls, and resource usage to prevent unexpected bills.

## Overview

The Cost Monitor Hook skill helps developers avoid surprise cloud bills by monitoring and alerting on expensive operations. It tracks API calls to metered services, cloud resource provisioning, and compute-intensive operations.

This skill is essential for teams working with paid APIs and cloud services where costs can accumulate quickly.

## Usage

### Start Tracking

```bash
skill cost-monitor-hook --track
```

### Set Alerts

```bash
skill cost-monitor-hook --alert --threshold 10.00
skill cost-monitor-hook --alert --threshold 100 --service openai
```

### Generate Report

```bash
skill cost-monitor-hook --report
```

### Dry Run with Cost Estimate

```bash
skill cost-monitor-hook --estimate -- my-script.sh
```

## Tracked Services

### Cloud Providers
- AWS EC2, RDS, Lambda, S3
- GCP Compute, Cloud SQL, BigQuery
- Azure VM, Cosmos DB, Functions

### AI/ML Services
- OpenAI API (GPT-4, embeddings)
- Anthropic API
- Hugging Face Inference
- Stability AI

### Other Services
- Stripe API
- Twilio
- SendGrid
- Database services (PlanetScale, Neon)

## Cost Tracking Examples

### Estimated Costs Before Execution

```
$ skill cost-monitor-hook --estimate -- python batch-process.py

ESTIMATED COSTS:
  OpenAI GPT-4 API: ~$2.50 (1000 requests × $0.03/1k tokens)
  AWS S3 Storage: ~$0.10 (1GB × $0.023/GB)
  Database Queries: ~$0.15 (10000 queries × $0.01/1k)

TOTAL ESTIMATED: ~$2.75
```

### Live Cost Tracking

```
$ skill cost-monitor-hook --track -- python process-images.py

[COST TRACKING]
Session started: 2024-01-15T10:00:00Z

Current costs:
  OpenAI Vision API: $1.23 (41 calls × $0.03/image)
  AWS S3: $0.05 (2.3GB transfer)
  Total: $1.28

Alert threshold: $5.00
Remaining budget: $3.72
```

## Cost Optimization Suggestions

The skill provides recommendations like:

```
COST OPTIMIZATION OPPORTUNITIES:

1. Cache OpenAI responses
   - Similar prompts detected 15+ times
   - Potential savings: ~$0.50/session

2. Use GPT-3.5-turbo for simple tasks
   - 23 calls using GPT-4 for simple queries
   - Potential savings: ~$1.20/session

3. Batch S3 uploads
   - 50 individual PUT requests detected
   - Potential savings: 80% on request costs
```

## Configuration

Create `.cost-monitor.yaml`:

```yaml
services:
  openai:
    enabled: true
    model_costs:
      gpt-4: 0.03
      gpt-4-turbo: 0.01
      gpt-3.5-turbo: 0.001
  aws:
    enabled: true
    track:
      - ec2
      - s3
      - lambda

alerts:
  threshold: 10.00
  warning_percent: 0.8

caching:
  enabled: true
  ttl: 3600
```

## Requirements

- OpenCode agent environment
- Access to execute commands
- Optional: service API keys for accurate pricing