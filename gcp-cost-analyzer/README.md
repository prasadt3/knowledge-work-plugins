# GCP Cost Analyzer Plugin

A cost analysis plugin for Claude Code that helps you analyze GCP bills, track project costs over time, identify savings opportunities, and right-size infrastructure. Works with billing exports, gcloud CLI, and Terraform to provide actionable cost optimization.

## Installation

```
claude plugins add gcp-cost-analyzer
```

## What It Does

This plugin transforms Claude into a GCP cost optimization partner. It helps you understand your cloud bill, find waste, right-size resources, and track savings over time.

### With gcloud CLI Access

Connect your GCP projects via `gcloud auth login` for the best experience. Claude will:

- Query live resource configurations across all projects
- Check utilization metrics via Cloud Monitoring
- Identify zombie resources and over-provisioned instances
- Provide exact `gcloud` commands to implement savings

### With Billing CSV Exports

Download billing exports from Cloud Console > Billing > Reports and pass them to Claude for analysis. Claude can break down costs by service, project, SKU, and label.

### With Terraform

If your infrastructure is managed via Terraform, Claude can suggest tfvars changes for cost-optimized configurations and help you switch between cost profiles (lean, standard, workshop).

## Commands

| Command | What it does |
|---------|-------------|
| `/bill-analysis` | Analyze a GCP billing CSV or live billing data — break down by service, project, SKU |
| `/project-costs` | Deep dive into a specific project's costs, resources, and trends over time |
| `/savings-finder` | Find specific savings with exact gcloud commands and Terraform changes |
| `/cost-trend` | Track cost trends over time, measure optimization impact, forecast future costs |
| `/resource-audit` | Audit all resources across projects for waste — idle, over-provisioned, orphaned |

## Skills

| Skill | Description |
|-------|-------------|
| `gcp-billing-analysis` | GCP pricing models, billing export formats, service cost drivers, and anomaly patterns |
| `cost-optimization-patterns` | 10 proven optimization patterns with detection, implementation, savings, and risks |

## Agents

| Agent | Description |
|-------|-------------|
| `cost-monitor` | Continuous cost monitoring — daily tracking, anomaly detection, budget alerts |
| `savings-advisor` | Proactive savings discovery — right-sizing, pricing optimization, architecture review |

## Example Workflows

### Monthly Bill Review

```
You: /bill-analysis 2026-01

Claude: [Fetches billing data or analyzes CSV]
       → [Breaks down: Cloud Run $6,484 (49%), Cloud SQL $2,243 (17%), Redis $1,163 (9%)]
       → [Flags anomaly: Spanner charges but no Spanner instances — Firestore billing issue]
       → [Recommends: Focus optimization on Cloud Run (largest cost driver)]
```

### Finding Savings

```
You: /savings-finder

Claude: [Scans all projects and resources]
       → [Quick Wins: Delete unused GKE cluster ($310/month), release static IPs ($7/month)]
       → [Right-Sizing: Cloud Run 8→2 vCPU ($3,200/month), Cloud SQL downsize ($800/month)]
       → [Provides exact gcloud commands for each recommendation]
       → [Total savings identified: $5,200/month]
```

### Resource Audit

```
You: /resource-audit all

Claude: [Scans Cloud Run, Cloud SQL, GKE, Redis, networking, storage]
       → [🔴 Critical: 2 unused resources costing $450/month]
       → [⚠️ Warning: 3 over-provisioned resources, potential $1,200/month savings]
       → [✅ Healthy: 8 resources properly sized]
       → [Waste Score: 5/10 — room for improvement]
```

### Tracking Optimization Progress

```
You: /cost-trend

Claude: [Compares January baseline to current month]
       → [January: $13,311 → March: $3,850 (71% reduction)]
       → [Charts monthly trend with annotations for each optimization]
       → [Forecasts: On track for $46,200 annual savings]
```

## Data Sources

> If you see unfamiliar placeholders or need to check which tools are connected, see [CONNECTORS.md](CONNECTORS.md).

This plugin works best when connected to your GCP infrastructure:

- **gcloud CLI**: Resource configurations, project inventory, live metrics
- **Billing CSV exports**: Detailed cost breakdowns by service, SKU, project
- **BigQuery billing export**: Programmatic billing analysis (most detailed)
- **Cloud Monitoring**: CPU, memory, and utilization metrics
- **Terraform state**: Infrastructure configurations and drift detection

Configure `gcloud auth login` and ensure the CLI has access to your projects for the best experience.
