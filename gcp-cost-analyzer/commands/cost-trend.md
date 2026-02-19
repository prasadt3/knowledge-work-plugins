---
description: Visualize GCP cost trends over time — month-over-month changes, growth rates, and forecast future costs
argument-hint: "[period]"
---

# Cost Trend Analysis

> If you see unfamiliar placeholders or need to check which tools are connected, see [CONNECTORS.md](../CONNECTORS.md).

Track GCP costs over time to identify trends, verify optimization impact, and forecast future spending.

## Usage

```
/cost-trend [period]
```

### Arguments

- `period` — Time range to analyze (default: 6 months)
  - `3m` — Last 3 months
  - `6m` — Last 6 months (default)
  - `12m` — Last 12 months
  - `ytd` — Year to date

## Workflow

### 1. Gather Historical Cost Data

**Option A: Multiple CSV exports**
If user has billing CSVs from multiple months, read and aggregate each.

**Option B: BigQuery billing export**
```sql
SELECT
  FORMAT_DATE('%Y-%m', usage_start_time) as month,
  service.description as service,
  project.id as project,
  SUM(cost) as total_cost,
  SUM(IFNULL((SELECT SUM(c.amount) FROM UNNEST(credits) c), 0)) as total_credits
FROM `PROJECT.dataset.gcp_billing_export_v1_XXXXXX`
WHERE usage_start_time >= TIMESTAMP_SUB(CURRENT_TIMESTAMP(), INTERVAL 180 DAY)
GROUP BY month, service, project
ORDER BY month, total_cost DESC
```

**Option C: gcloud logging**
Use billing budget alerts and cost anomaly data.

### 2. Monthly Cost Trend

```
MONTHLY COST TREND
═══════════════════════════════════════════════════════════

Month       Total      MoM Change    Annualized
─────────────────────────────────────────────────────────
Sep 2025    $11,200    —             $134,400
Oct 2025    $11,800    +$600 (+5%)   $141,600
Nov 2025    $12,400    +$600 (+5%)   $148,800
Dec 2025    $13,100    +$700 (+6%)   $157,200
Jan 2026    $13,311    +$211 (+2%)   $159,732
Feb 2026*   $5,800     -$7,511(-56%) $69,600   ← optimization
Mar 2026†   $3,850     -$1,950(-34%) $46,200   ← full effect

* Partial optimization month
† Projected (first full optimized month)

Trend: ↓ DECREASING (post-optimization)
Growth rate (pre-optimization): +4.5%/month
Growth rate (post-optimization): -45% step change
```

### 3. Service-Level Trends

```
SERVICE COST TRENDS (Monthly)
═══════════════════════════════════════════════════════════

Cloud Run:
  Sep     Oct     Nov     Dec     Jan     Feb*    Mar†
  $5,200  $5,500  $5,900  $6,200  $6,484  $2,800  $1,800
  Trend: ↓ -72% (right-sized instances)

Cloud SQL:
  Sep     Oct     Nov     Dec     Jan     Feb*    Mar†
  $2,100  $2,100  $2,200  $2,200  $2,243  $1,800  $900
  Trend: ↓ -60% (downsized + deleted unused)

Redis:
  Sep     Oct     Nov     Dec     Jan     Feb*    Mar†
  $1,100  $1,100  $1,150  $1,150  $1,163  $800    $350
  Trend: ↓ -70% (16GB → 5GB)
```

### 4. Project-Level Trends

```
PROJECT COST TRENDS (Monthly)
═══════════════════════════════════════════════════════════

Project                      Jan 2026    Mar 2026†   Change
─────────────────────────────────────────────────────────
logical-light-427516-v5      $10,878     $2,500      -77%
agentman-terraformed         $1,945      $800        -59%
crawl-websites               $217        $200        -8%
agentman-public-mcp-servers  $167        $80         -52%
Other                        $104        $100        -4%
─────────────────────────────────────────────────────────
TOTAL                        $13,311     $3,680      -72%
```

### 5. Cost Velocity

Track the rate of cost change:

```
COST VELOCITY (Rate of Change)
═══════════════════════════════════════════════════════════

Pre-Optimization (Sep-Jan):
  Average monthly increase: +$528/month (+4.5%)
  Annualized trajectory: $19,000/year increase
  Projected Dec 2026 bill: $18,600 (if unchecked)

Post-Optimization (Feb onward):
  Step-change reduction: -$9,461/month (-71%)
  New baseline: ~$3,850/month
  Projected annual cost: ~$46,200

12-Month Savings vs Trajectory: ~$113,500
```

### 6. Forecast

```
COST FORECAST (Next 6 Months)
═══════════════════════════════════════════════════════════

Assumptions:
- Base: Current optimized infrastructure
- Growth: 5% monthly traffic increase
- New services: None planned

Month       Forecast    Confidence    Notes
─────────────────────────────────────────────────────────
Mar 2026    $3,850      High          First full optimized month
Apr 2026    $3,950      High          Slight growth
May 2026    $4,050      Medium        Cloud Run may scale
Jun 2026    $4,150      Medium
Jul 2026    $4,300      Low           Depends on traffic
Aug 2026    $4,450      Low

6-Month Total: ~$24,750
vs. Pre-optimization: ~$84,000
Savings: ~$59,250 over 6 months
```

### 7. Optimization Impact Tracking

If optimizations were recently applied, show before/after:

```
OPTIMIZATION IMPACT
═══════════════════════════════════════════════════════════

Action                          Before      After       Savings
─────────────────────────────────────────────────────────
Cloud Run lean config           $6,484      $1,800      $4,684
Cloud SQL downsizing            $2,243      $900        $1,343
Redis downsizing                $1,163      $350        $813
Firestore deletion              $1,010      $0          $1,010
GKE test cluster deletion       $648        $200        $448
Cloud Composer deletion         $370        $0          $370
Security Command Center         $527        $0          $527
MCP servers min=0               $167        $80         $87
─────────────────────────────────────────────────────────
TOTAL                           $12,612     $3,330      $9,282
─────────────────────────────────────────────────────────
Monthly savings: $9,282/month
Annual savings: $111,384/year
```

## Output Format

```
═══════════════════════════════════════════════════════════
GCP COST TREND ANALYSIS
Period: [Date Range]
Current Monthly Cost: $X,XXX
Trend: ↑ Increasing / → Stable / ↓ Decreasing
═══════════════════════════════════════════════════════════

📈 MONTHLY TREND [table]
📊 BY SERVICE [service trends]
🏢 BY PROJECT [project trends]
⚡ COST VELOCITY [rate of change]
🔮 FORECAST [projected costs]
✅ OPTIMIZATION IMPACT [before/after if applicable]
═══════════════════════════════════════════════════════════
```

## Related Commands

- `/bill-analysis` — Detailed breakdown of a single month
- `/project-costs` — Trend for a specific project
- `/savings-finder` — Find new optimization opportunities
- `/resource-audit` — Check if optimizations are holding
