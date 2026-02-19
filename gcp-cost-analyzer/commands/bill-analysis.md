---
description: Analyze GCP billing data from CSV exports or live billing API to break down costs by service, project, and SKU
argument-hint: "[csv-path or period]"
---

# GCP Bill Analysis

> If you see unfamiliar placeholders or need to check which tools are connected, see [CONNECTORS.md](../CONNECTORS.md).

Analyze your Google Cloud Platform bill to understand where money is going, broken down by service, project, SKU, and label.

## Usage

```
/bill-analysis [csv-path or period]
```

### Arguments

- `csv-path` — Path to a GCP billing export CSV file (from Cloud Console > Billing > Reports > Download CSV)
- `period` — Time period for live analysis: `last-month`, `this-month`, `90d`, `ytd`
- If no argument, defaults to analyzing the current month via gcloud CLI

## Workflow

### 1. Load Billing Data

**Option A: CSV Export (Recommended for detailed analysis)**

If user provides a CSV path:
- Read the CSV file using the Read tool
- Parse columns: `Service description`, `SKU description`, `Cost ($)`, `Project ID`, `Usage start date`, `Usage end date`, `Labels`
- Handle both standard export and cost table export formats
- GCP billing CSVs may use different column names depending on export type

Common GCP billing CSV column patterns:
```
Standard Export:
- Billing account ID, Project ID, Service description, SKU description, Cost ($), Credits ($)

Cost Table Export:
- Service, SKU, Project, Cost, Credits, Usage amount, Usage unit
```

**Option B: gcloud CLI (For quick checks)**

If no CSV provided, use gcloud commands:
```bash
# List billing accounts
gcloud billing accounts list

# Get cost breakdown for a project
gcloud billing projects describe PROJECT_ID

# Use BigQuery billing export if configured
bq query --use_legacy_sql=false '
  SELECT
    service.description as service,
    SUM(cost) as total_cost
  FROM `PROJECT.dataset.gcp_billing_export_v1_XXXXXX`
  WHERE DATE(usage_start_time) >= DATE_SUB(CURRENT_DATE(), INTERVAL 30 DAY)
  GROUP BY service
  ORDER BY total_cost DESC
'
```

### 2. Aggregate by Service

Group costs by GCP service:

```
GCP BILL ANALYSIS
Period: [Date Range]
Total Cost: $XX,XXX.XX

BY SERVICE
═══════════════════════════════════════════════════════════
Service                          Cost        % of Total
─────────────────────────────────────────────────────────
Cloud Run                        $X,XXX.XX      XX.X%
Cloud SQL                        $X,XXX.XX      XX.X%
Compute Engine                   $X,XXX.XX      XX.X%
Cloud Memorystore (Redis)        $X,XXX.XX      XX.X%
Networking                       $XXX.XX         X.X%
Cloud Storage                    $XXX.XX         X.X%
Artifact Registry                $XXX.XX         X.X%
Other                            $XXX.XX         X.X%
─────────────────────────────────────────────────────────
TOTAL                            $XX,XXX.XX    100.0%
```

### 3. Aggregate by Project

Group costs by GCP project:

```
BY PROJECT
═══════════════════════════════════════════════════════════
Project                          Cost        % of Total
─────────────────────────────────────────────────────────
logical-light-427516-v5          $X,XXX.XX      XX.X%
agentman-terraformed             $X,XXX.XX      XX.X%
crawl-websites                   $XXX.XX         X.X%
agentman-public-mcp-servers      $XXX.XX         X.X%
─────────────────────────────────────────────────────────
TOTAL                            $XX,XXX.XX    100.0%
```

### 4. Top SKUs (Line Items)

Show the most expensive individual line items:

```
TOP 20 SKUs BY COST
═══════════════════════════════════════════════════════════
Service / SKU                              Cost      Project
─────────────────────────────────────────────────────────
Cloud SQL / db-custom-4-16384 (vCPU)      $XXX.XX    project-a
Cloud Run / CPU Allocation Time           $XXX.XX    project-a
Compute Engine / N1 Predefined (RAM)      $XXX.XX    project-b
Cloud Run / Memory Allocation Time        $XXX.XX    project-a
Cloud Memorystore / Redis Standard HA     $XXX.XX    project-a
...
```

### 5. Credits and Discounts

Show any credits applied:

```
CREDITS & DISCOUNTS
═══════════════════════════════════════════════════════════
Credit Type                      Amount
─────────────────────────────────────────────────────────
Sustained use discount           -$XXX.XX
Committed use discount           -$XXX.XX
Promotional credits              -$XXX.XX
─────────────────────────────────────────────────────────
Total Credits                    -$XXX.XX
Net Cost (after credits)         $XX,XXX.XX
```

### 6. Cost Anomalies

Flag unusual items:

```
ANOMALIES & ALERTS
═══════════════════════════════════════════════════════════
🔴 Cloud Spanner: $1,010 — No Spanner instances found.
   May be Firestore in Datastore mode billing as Spanner.
   Action: Check `gcloud firestore databases list`

🟡 Cloud Run: $6,484 — 49% of total bill.
   Consider right-sizing instances or using horizontal scaling.

🟡 Cloud SQL: $2,243 — Verify instance tiers match actual usage.
   Run `/resource-audit cloud-sql` for details.
```

### 7. Recommendations

```
RECOMMENDATIONS
═══════════════════════════════════════════════════════════
1. Right-size Cloud Run instances
   Current: 8 vCPU / 16 GB → Recommended: 2 vCPU / 4 GB
   Potential savings: ~$4,000/month
   Command: /savings-finder cloud-run

2. Enable committed use discounts for Cloud SQL
   Stable workloads qualify for 1-year or 3-year CUDs
   Potential savings: ~$400/month

3. Review idle resources
   Command: /resource-audit all
```

## Output Format

```
═══════════════════════════════════════════════════════════
GCP BILL ANALYSIS
Period: [Date Range]
Total Cost: $XX,XXX.XX | Credits: -$X,XXX.XX | Net: $XX,XXX.XX
═══════════════════════════════════════════════════════════

📊 BY SERVICE [breakdown table]
🏢 BY PROJECT [breakdown table]
📋 TOP SKUs [detailed line items]
💰 CREDITS & DISCOUNTS [credit summary]
⚠️  ANOMALIES [flagged items]
💡 RECOMMENDATIONS [actionable next steps]
═══════════════════════════════════════════════════════════
```

## Data Sources

Priority order for billing data:
1. **CSV export** — Most detailed, includes SKU-level data
2. **BigQuery billing export** — If configured, query directly
3. **gcloud CLI** — For quick project-level checks
4. **Cloud Console screenshots** — If user provides screenshots, read and analyze

## Related Commands

- `/project-costs` — Track costs for a specific project over time
- `/cost-trend` — Visualize cost trends month-over-month
- `/savings-finder` — Deep dive into savings for a specific service
- `/resource-audit` — Audit running resources for waste
