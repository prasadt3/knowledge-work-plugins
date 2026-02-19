---
description: Track and compare costs for a specific GCP project over time with service-level breakdown
argument-hint: "<project-id> [period]"
---

# Project Costs

> If you see unfamiliar placeholders or need to check which tools are connected, see [CONNECTORS.md](../CONNECTORS.md).

Deep dive into costs for a specific GCP project. Track spending over time, break down by service and resource, and identify optimization opportunities.

## Usage

```
/project-costs <project-id> [period]
```

### Arguments

- `project-id` — Required. GCP project ID to analyze
- `period` — Optional. Time range (default: last 3 months)
  - `1m` — Last month
  - `3m` — Last 3 months (default)
  - `6m` — Last 6 months
  - `ytd` — Year to date

## Workflow

### 1. Gather Project Information

Use gcloud to get project details:
```bash
# Project info
gcloud projects describe PROJECT_ID

# List services enabled
gcloud services list --project=PROJECT_ID --enabled

# List running resources
gcloud run services list --project=PROJECT_ID
gcloud sql instances list --project=PROJECT_ID
gcloud compute instances list --project=PROJECT_ID
gcloud redis instances list --project=PROJECT_ID --region=REGION
gcloud container clusters list --project=PROJECT_ID
```

### 2. Current Resource Inventory

List all billable resources in the project:

```
RESOURCE INVENTORY: [project-id]
═══════════════════════════════════════════════════════════

Cloud Run Services:
  Service Name              Region      CPU    Memory  Min  Max
  ─────────────────────────────────────────────────────────
  agentman-studio-api       us-west2    2      4Gi     2    100
  agentman-runtime-api      us-west2    2      4Gi     2    50
  agentlens-worker          us-west2    1      2Gi     1    10

Cloud SQL Instances:
  Instance Name             Tier                  Storage   HA
  ─────────────────────────────────────────────────────────
  coa-studio-prod           db-custom-4-16384     100GB     Yes
  agentman-autotest-prod    db-g1-small           10GB      No

Redis Instances:
  Instance Name             Tier          Size    HA
  ─────────────────────────────────────────────────────────
  prod-agentlens-redis      STANDARD_HA   5GB     Yes

GKE Clusters:
  Cluster Name              Nodes    Machine Type
  ─────────────────────────────────────────────────────────
  airflow-cluster-dec       2        e2-standard-4
```

### 3. Cost Breakdown by Service

```
COST BREAKDOWN: [project-id]
Period: [Date Range]
Total: $X,XXX.XX
═══════════════════════════════════════════════════════════

Service                     This Month   Last Month   Change
─────────────────────────────────────────────────────────
Cloud Run                   $X,XXX.XX    $X,XXX.XX    -XX%
Cloud SQL                   $X,XXX.XX    $X,XXX.XX    -XX%
Compute Engine              $XXX.XX      $XXX.XX      +X%
Cloud Memorystore           $XXX.XX      $XXX.XX      -XX%
Networking                  $XXX.XX      $XXX.XX      →
Cloud Storage               $XXX.XX      $XXX.XX      →
─────────────────────────────────────────────────────────
TOTAL                       $X,XXX.XX    $XX,XXX.XX   -XX%
```

### 4. Cost Per Resource

Map costs to specific resources:

```
COST PER RESOURCE
═══════════════════════════════════════════════════════════

Cloud Run:
  agentman-studio-api       $XXX.XX/month (CPU: $XXX, Memory: $XXX)
  agentman-runtime-api      $XXX.XX/month (CPU: $XXX, Memory: $XXX)
  agentlens-worker          $XXX.XX/month (CPU: $XX, Memory: $XX)

Cloud SQL:
  coa-studio-prod           $XXX.XX/month (Compute: $XXX, Storage: $XX)
  agentman-autotest-prod    $XX.XX/month  (Compute: $XX, Storage: $X)

Redis:
  prod-agentlens-redis      $XXX.XX/month
```

### 5. Month-over-Month Trend

```
MONTHLY COST TREND: [project-id]
═══════════════════════════════════════════════════════════

Month       Total      Cloud Run  Cloud SQL  Redis    Other
─────────────────────────────────────────────────────────
Oct 2025    $XX,XXX    $X,XXX     $X,XXX     $XXX     $XXX
Nov 2025    $XX,XXX    $X,XXX     $X,XXX     $XXX     $XXX
Dec 2025    $XX,XXX    $X,XXX     $X,XXX     $XXX     $XXX
Jan 2026    $XX,XXX    $X,XXX     $X,XXX     $XXX     $XXX
Feb 2026*   $X,XXX     $X,XXX     $XXX       $XXX     $XXX

* Partial month / projected

Trend: ↓ Decreasing (-XX% over period)
```

### 6. Optimization Recommendations

Generate project-specific recommendations:

```
OPTIMIZATION FOR [project-id]
═══════════════════════════════════════════════════════════

HIGH IMPACT:
1. Cloud Run right-sizing
   - Studio API: Consider 1 vCPU / 2Gi if CPU usage <50%
   - Savings: ~$XXX/month

2. Cloud SQL committed use discount
   - coa-studio-prod runs 24/7 — qualifies for 1-year CUD
   - Savings: ~$XXX/month (30% discount)

MEDIUM IMPACT:
3. Set min-instances=1 on low-traffic services
4. Enable autoscaling on Cloud SQL storage

LOW IMPACT:
5. Clean up old container images in Artifact Registry
6. Review network egress patterns
```

## Use Cases

- **Monthly review**: Track how project costs change month-to-month
- **Budget planning**: Understand cost drivers for capacity planning
- **Post-optimization verification**: Confirm savings after right-sizing
- **Multi-project comparison**: Run for each project to compare

## Related Commands

- `/bill-analysis` — Full bill analysis across all projects
- `/savings-finder` — Deep dive into savings for a specific service
- `/resource-audit` — Audit resources for waste and over-provisioning
- `/cost-trend` — Visualize trends across all projects
