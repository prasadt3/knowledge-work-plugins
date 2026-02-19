---
name: gcp-billing-analysis
description: Deep knowledge of GCP pricing models, billing export formats, cost allocation, and billing anomaly patterns. Use when analyzing GCP bills, understanding service cost drivers, interpreting billing exports, or diagnosing billing anomalies.
---

# GCP Billing Analysis & Cost Structure

## Overview

Understanding GCP billing is essential for managing cloud costs. GCP uses a complex pricing model with per-second billing, sustained use discounts, committed use discounts, and various pricing tiers across 100+ services.

This skill provides comprehensive knowledge of GCP billing structure, export formats, analysis techniques, and common cost patterns.

## GCP Pricing Models

### 1. On-Demand (Pay-as-you-go)

Most GCP services charge based on actual usage with per-second or per-minute billing:

- **Compute Engine**: Per-second billing (minimum 1 minute)
- **Cloud Run**: Per 100ms of CPU/memory allocation
- **Cloud SQL**: Per-hour billing for instances
- **Cloud Storage**: Per GB/month + per operation
- **BigQuery**: Per TB scanned (on-demand) or slot-hours (flat-rate)

### 2. Sustained Use Discounts (SUDs)

Automatic discounts for running Compute Engine resources consistently:

```
Usage       Discount
0-25%       0% (full price)
25-50%      20% off incremental usage
50-75%      40% off incremental usage
75-100%     60% off incremental usage

Effective discount for 100% usage: ~30%
```

Applies to: Compute Engine VMs, GKE nodes, Cloud SQL (partially)
Does NOT apply to: Cloud Run, App Engine, Cloud Functions

### 3. Committed Use Discounts (CUDs)

Pre-commit to a resource level for 1 or 3 years:

```
Resource-Based CUDs:
  1-year: 37% discount
  3-year: 55% discount
  Applies to: vCPU, memory for Compute Engine

Spend-Based CUDs:
  1-year: 25% discount
  3-year: 52% discount
  Applies to: Cloud SQL, Cloud Memorystore, more
```

### 4. Flat-Rate Pricing

Some services offer flat-rate alternatives:

- **BigQuery**: Flat-rate slots (predictable cost vs per-query)
- **Cloud Spanner**: Per-node pricing
- **GKE Autopilot**: Per-pod resource pricing

### 5. Free Tier

GCP offers always-free tier for many services:

```
Compute Engine:     1 e2-micro instance/month (US regions)
Cloud Storage:      5 GB Standard storage
BigQuery:           1 TB queries, 10 GB storage
Cloud Functions:    2M invocations, 400K GB-seconds
Cloud Run:          2M requests, 360K GB-seconds, 180K vCPU-seconds
Pub/Sub:            10 GB messages
Cloud Build:        120 build-minutes/day
Artifact Registry:  500 MB storage
```

## GCP Billing Export Formats

### Standard Billing Export (CSV)

Downloaded from Cloud Console > Billing > Reports > Download:

```csv
Billing account ID,Project ID,Project name,Service description,SKU description,Cost ($),Credits ($),Usage start date,Usage end date
XXXXX,project-id,Project Name,Cloud Run,CPU Allocation Time,123.45,0.00,2026-01-01,2026-01-31
```

Key columns:
- `Service description` — GCP service name (Cloud Run, Cloud SQL, etc.)
- `SKU description` — Specific line item (CPU Allocation Time, Standard Storage, etc.)
- `Cost ($)` — Gross cost before credits
- `Credits ($)` — Discounts and credits applied
- `Project ID` — Which project incurred the cost

### Cost Table Export (CSV)

More detailed export from Billing > Cost Table:

```csv
Service,SKU,Project,Cost,Credits,Subtotal,Usage amount,Usage unit,Labels
Cloud Run,CPU Allocation Time,project-id,123.45,-5.00,118.45,50000,vCPU-second,env:prod
```

Additional columns:
- `Subtotal` — Cost after credits
- `Usage amount` + `Usage unit` — Actual resource consumption
- `Labels` — User-defined labels for cost allocation

### BigQuery Billing Export

Most detailed, recommended for programmatic analysis:

```sql
-- Schema: gcp_billing_export_v1_XXXXXX
SELECT
  billing_account_id,
  service.id as service_id,
  service.description as service_name,
  sku.id as sku_id,
  sku.description as sku_name,
  project.id as project_id,
  project.name as project_name,
  location.region,
  usage_start_time,
  usage_end_time,
  cost,
  currency,
  usage.amount as usage_amount,
  usage.unit as usage_unit,
  usage.amount_in_pricing_units,
  usage.pricing_unit,
  credits,  -- ARRAY of credit structs
  labels,   -- ARRAY of key-value label structs
  cost_type -- regular, tax, adjustment, rounding_error
FROM `project.dataset.gcp_billing_export_v1_XXXXXX`
```

## Common GCP Services and Their Cost Drivers

### Cloud Run

```
Cost Components:
  CPU:    $0.00002400 per vCPU-second (billable when processing requests)
  Memory: $0.00000250 per GiB-second
  Requests: $0.40 per million requests (first 2M free)

Cost Drivers:
  - min-instances: Pre-allocated instances always incur CPU+memory charges
  - CPU allocation: "always allocated" vs "only during requests"
  - Concurrency: Lower concurrency = more instances = higher cost
  - Cold starts: If min=0, first request has latency but saves money

Monthly Cost Formula (per service):
  Base = min_instances × (cpu_cost + memory_cost) × seconds_in_month
  Variable = additional_instances × (cpu_cost + memory_cost) × active_seconds
  Total = Base + Variable + Request charges

Example:
  2 vCPU, 4 GiB, min=2, always-on:
  CPU: 2 × 2 × $0.0000240 × 2,592,000 = $248.83
  Mem: 2 × 4 × $0.0000025 × 2,592,000 = $51.84
  Monthly: ~$301 per service (minimum)
```

### Cloud SQL

```
Cost Components:
  Instance: Hourly charge based on machine type (vCPUs + RAM)
  Storage: Per GB/month ($0.17/GB SSD, $0.09/GB HDD)
  Network: Egress charges for cross-region traffic
  Backups: Per GB/month ($0.08/GB)
  HA: Doubles instance cost (standby replica)

Common Machine Types:
  db-g1-small:           ~$25/month (shared vCPU, 1.7 GB)
  db-custom-1-3840:      ~$50/month (1 vCPU, 3.75 GB)
  db-custom-2-8192:      ~$130/month (2 vCPU, 8 GB)
  db-custom-4-16384:     ~$260/month (4 vCPU, 16 GB)
  db-custom-8-32768:     ~$520/month (8 vCPU, 32 GB)
  db-custom-16-65536:    ~$1,040/month (16 vCPU, 64 GB)

  With HA: Multiply by ~2x

Right-Sizing Signals:
  - CPU utilization <30% average → can likely downsize
  - Memory usage <50% → can likely downsize
  - Connection count low → may not need large instance
  - Storage <50% of allocated → review auto-resize settings
```

### Compute Engine (GKE Nodes)

```
Cost Components:
  Instance: Per-second billing based on machine type
  Persistent Disk: Per GB/month ($0.04/GB standard, $0.17/GB SSD)
  Network: Egress charges
  GKE Management Fee: $0.10/hour per cluster (~$73/month)

Common Machine Types:
  e2-micro:        ~$7/month (0.25 vCPU, 1 GB)
  e2-small:        ~$15/month (0.5 vCPU, 2 GB)
  e2-medium:       ~$25/month (1 vCPU, 4 GB)
  e2-standard-2:   ~$49/month (2 vCPU, 8 GB)
  e2-standard-4:   ~$98/month (4 vCPU, 16 GB)
  e2-standard-8:   ~$195/month (8 vCPU, 32 GB)

  Preemptible/Spot: 60-91% cheaper (but can be interrupted)

GKE Specific:
  Autopilot: Pay per pod resources (no node management)
  Standard: Pay for full nodes (even if underutilized)
  Autopilot is often cheaper for variable workloads
```

### Cloud Memorystore (Redis)

```
Cost Components:
  Instance: Per GB/hour based on tier
  Network: Minimal for same-region traffic

Pricing (us-west2):
  BASIC tier: ~$0.049/GB/hour (~$35/GB/month)
  STANDARD_HA tier: ~$0.068/GB/hour (~$49/GB/month)

  STANDARD_HA includes automatic failover replica

Minimum Sizes:
  BASIC: 1 GB minimum
  STANDARD_HA: 5 GB minimum (with replicas)

Examples:
  5 GB BASIC:        ~$175/month
  5 GB STANDARD_HA:  ~$350/month (includes HA)
  16 GB STANDARD_HA: ~$1,120/month
```

### Networking

```
Key Cost Drivers:
  Egress: $0.12/GB for internet egress (first 1 TB)
  Inter-region: $0.01/GB between regions
  Load Balancer: ~$0.025/hour + $0.008/GB processed
  Static IP: $0.010/hour if NOT attached (~$7.20/month unused)
  Cloud NAT: $0.044/hour + $0.045/GB processed

  Cloud CDN: $0.02-0.08/GB depending on region
  Cloud Armor: $5/policy/month + $0.75/million requests
```

## Billing Anomaly Patterns

### Pattern 1: Firestore Datastore Mode Billing as Spanner

```
Symptom: Cloud Spanner charges but no Spanner instances
Cause: Firestore databases in "Datastore mode" bill under Spanner
Detection:
  gcloud spanner instances list → empty
  gcloud firestore databases list → found databases in DATASTORE_MODE
Fix: Delete unused Firestore databases
```

### Pattern 2: Security Command Center Premium

```
Symptom: Large "Security Command Center" charge ($500+/month)
Cause: Premium tier auto-enabled or forgotten
Detection: Check organization settings
Fix: Disable or downgrade to Standard tier (free)
```

### Pattern 3: Zombie Cloud Composer

```
Symptom: Cloud Composer charges despite not using it
Cause: Composer environments left running (GKE + Cloud SQL + Storage)
Detection:
  gcloud composer environments list --locations=all
Fix: Delete unused environments
Impact: $300-500+/month per environment
```

### Pattern 4: Over-provisioned Cloud Run

```
Symptom: Cloud Run is largest cost item
Cause: Large instances (8 vCPU) with high min-instances
Detection:
  gcloud run services describe SERVICE → check resources
Fix: Right-size to 1-2 vCPU, use horizontal scaling
Impact: 50-75% reduction in Cloud Run costs
```

### Pattern 5: Orphaned Resources

```
Common orphaned resources:
  - Static IPs not attached to anything ($7.20/month each)
  - Load balancer components pointing to deleted services
  - Persistent disks not attached to VMs
  - Old container images in Artifact Registry
  - Unused GKE clusters with running nodes
Detection:
  gcloud compute addresses list --filter="status=RESERVED"
  gcloud compute disks list --filter="-users:*"
```

## Cost Allocation Best Practices

### Labels

Apply labels to all resources for cost tracking:

```
Required Labels:
  environment: prod | staging | dev
  team: engineering | marketing | data
  service: api | worker | frontend
  cost-center: CC-001 | CC-002

gcloud run services update SERVICE \
  --update-labels=environment=prod,team=engineering,service=api
```

### Billing Budgets

Set up budgets for proactive alerting:

```bash
# Create budget via gcloud
gcloud billing budgets create \
  --billing-account=BILLING_ACCOUNT_ID \
  --display-name="Monthly Alert" \
  --budget-amount=5000 \
  --threshold-rules-from-file=thresholds.json
```

Recommended thresholds:
- 50% of budget: Informational
- 80% of budget: Warning
- 100% of budget: Critical
- 120% of budget: Emergency

### Cost Exports

Always enable BigQuery billing export for detailed analysis:

```
Cloud Console > Billing > Billing Export > BigQuery Export
  - Standard usage cost: Detailed line items
  - Detailed usage cost: Resource-level data
  - Pricing: Current pricing information
```

## Analysis Techniques

### Pareto Analysis (80/20 Rule)

Typically 2-3 services account for 80% of the bill:

```
Rank services by cost:
1. Cloud Run:    $6,484 (49%) ← Optimize this first
2. Cloud SQL:    $2,243 (17%) ← Then this
3. Redis:        $1,163 (9%)  ← Then this
   Subtotal:     $9,890 (74%) of $13,311 total

Focus optimization on top 3 services for maximum impact.
```

### Cost per Customer/User

```
Monthly GCP Cost: $3,850
Active Customers: 500

Cost per Customer: $7.70/month
Revenue per Customer: $50/month
Infrastructure Margin: 84.6% (healthy)

Target: Infrastructure should be <20% of revenue
```

### Month-over-Month Growth Rate

```
Cost Growth Rate = (This Month - Last Month) / Last Month × 100

If cost growth > revenue growth → investigate
If cost growth < revenue growth → healthy scaling

Example:
  Revenue grew 15% MoM
  Costs grew 5% MoM
  → Improving unit economics ✅
```

## Tools and Commands Reference

### Quick Cost Check Commands

```bash
# List all projects and their billing
gcloud projects list
gcloud billing projects describe PROJECT_ID

# Cloud Run costs (check instance config)
gcloud run services list --project=PROJECT
gcloud run services describe SERVICE --region=REGION

# Cloud SQL costs (check tier)
gcloud sql instances list --project=PROJECT
gcloud sql instances describe INSTANCE --format="value(settings.tier)"

# Redis costs (check size)
gcloud redis instances list --project=PROJECT --region=REGION

# GKE costs (check nodes)
gcloud container clusters list --project=PROJECT
gcloud compute instances list --project=PROJECT

# Networking costs (check for waste)
gcloud compute addresses list --project=PROJECT --filter="status=RESERVED"
gcloud compute forwarding-rules list --project=PROJECT
```

### Cost Monitoring Setup

```bash
# Enable billing export to BigQuery (do once)
# Cloud Console > Billing > Billing Export > BigQuery Export

# Create budget alerts
gcloud billing budgets create \
  --billing-account=ACCOUNT \
  --display-name="GCP Monthly Budget" \
  --budget-amount=4000 \
  --threshold-rules=percent=0.5,basis=CURRENT_SPEND \
  --threshold-rules=percent=0.8,basis=CURRENT_SPEND \
  --threshold-rules=percent=1.0,basis=CURRENT_SPEND

# Set up Pub/Sub notifications for budget alerts
gcloud billing budgets update BUDGET_ID \
  --notifications-rule-pubsub-topic=projects/PROJECT/topics/billing-alerts
```

## Conclusion

Effective GCP cost analysis requires:

1. **Visibility** — Export billing data and apply labels
2. **Understanding** — Know what drives costs for each service
3. **Monitoring** — Set budgets and alerts
4. **Optimization** — Right-size, use CUDs, eliminate waste
5. **Tracking** — Measure savings impact over time

The biggest savings typically come from:
- Right-sizing over-provisioned instances (30-70% savings)
- Deleting unused resources (100% savings on waste)
- Committed use discounts (25-55% on stable workloads)
- Architectural changes (horizontal vs vertical scaling)
