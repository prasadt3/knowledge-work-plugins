---
description: Comprehensive real-time financial health dashboard for startup founders
argument-hint: ""
---

# Financial Snapshot Dashboard

Get a complete view of your startup's financial health in one comprehensive dashboard. Combines burn rate, runway, revenue metrics, and key startup KPIs.

## Usage

```
/financial-snapshot
```

No arguments needed - pulls all data from Mercury Bank and calculates key metrics.

## Workflow

### 1. Current Cash Position

Use Mercury MCP to fetch real-time balance:

```
CASH POSITION
==================
Current Balance: $XXX,XXX
Available Balance: $XXX,XXX (excluding pending)
Last Updated: [Timestamp]

Account Breakdown:
- Operating Account: $XXX,XXX
- Reserve Account: $XXX,XXX (if applicable)
```

### 2. Burn Rate Analysis

Either use cached `/burn-rate` result or calculate fresh:

```
BURN RATE (Last 3 Months)
==================
Current Month: $XX,XXX/month
Prior Month: $XX,XXX/month
3-Month Average: $XX,XXX/month

Trend: ↑ Increasing / → Stable / ↓ Decreasing
Month-over-Month: +/- $X,XXX (+/- X.X%)
```

### 3. Cash Runway

Calculate using current balance and burn:

```
RUNWAY
==================
Months Remaining: X.X months
Zero Cash Date: [Month DD, YYYY]

Status: 🟢 Healthy (>12mo) / 🟡 Monitor (6-12mo) / 🔴 Critical (<6mo)
```

### 4. Revenue Metrics

Pull revenue from Mercury deposits or ask user:

```
REVENUE (MRR/ARR)
==================
Monthly Recurring Revenue: $XX,XXX
Annual Run Rate: $XXX,XXX
Month-over-Month Growth: +X.X%

Top Revenue Sources:
1. [Customer/Product]: $XX,XXX
2. [Customer/Product]: $XX,XXX
3. [Customer/Product]: $XX,XXX
```

If revenue data is not in Mercury:
> Revenue data not found in Mercury transactions. Please provide your current MRR or monthly revenue.

### 5. Unit Economics

Calculate key efficiency metrics:

```
UNIT ECONOMICS
==================
Gross Margin: XX% ([Revenue - COGS] / Revenue)
CAC (Customer Acquisition Cost): $X,XXX
LTV (Lifetime Value): $XX,XXX
LTV:CAC Ratio: X.X:1 (Target: >3:1)

Burn Multiple: X.Xx ([Net Burn] / [Net New ARR])
- <1.5x: Excellent capital efficiency
- 1.5-3x: Good
- >3x: Needs optimization
```

### 6. Operating Efficiency

Analyze spend distribution:

```
OPERATING EFFICIENCY
==================
Revenue as % of Burn: XX%
Months to Profitability: XX months (at current growth rate)

Spend Breakdown:
- Payroll: XX% ($XX,XXX)
- Engineering/Infrastructure: XX% ($XX,XXX)
- Sales & Marketing: XX% ($XX,XXX)
- General & Admin: XX% ($XX,XXX)
```

### 7. Key Metrics Summary

Present critical startup KPIs:

```
KEY METRICS
==================
🏦 Cash: $XXX,XXX
📉 Burn: $XX,XXX/month
⏱️  Runway: X.X months
📈 MRR: $XX,XXX
📊 Growth: +X.X% MoM
💰 Burn Multiple: X.Xx
🎯 LTV:CAC: X.X:1
💵 Gross Margin: XX%
```

### 8. Growth Projections

Model next 12 months:

```
12-MONTH PROJECTION
==================
Assumptions:
- Revenue growth: X% monthly
- Burn rate: Flat / Growing X% / Decreasing X%

Month    Revenue    Burn      Cash       Runway
------   -------    -------   -------    ------
Mar 26   $XX,XXX    $XX,XXX   $XXX,XXX   X.X mo
Apr 26   $XX,XXX    $XX,XXX   $XXX,XXX   X.X mo
May 26   $XX,XXX    $XX,XXX   $XXX,XXX   X.X mo
...

Profitability Date: [Month YYYY] (if trajectory continues)
Cash-out Date: [Month YYYY] (if no additional funding)
```

### 9. Health Score

Calculate composite health score (0-100):

```
FINANCIAL HEALTH SCORE: XX/100

Score Breakdown:
✓ Runway: XX/25 pts (>12mo=25, 9-12mo=20, 6-9mo=15, <6mo=5)
✓ Growth: XX/25 pts (>15% MoM=25, 10-15%=20, 5-10%=15, <5%=10)
✓ Efficiency: XX/25 pts (Burn mult <1.5=25, 1.5-2=20, 2-3=15, >3=10)
✓ Unit Economics: XX/25 pts (LTV:CAC >3=25, 2-3=20, 1-2=15, <1=10)

Overall: 🟢 Excellent (80-100) / 🟡 Good (60-79) / 🟠 Fair (40-59) / 🔴 Poor (<40)
```

### 10. Action Items

Generate prioritized recommendations:

```
RECOMMENDED ACTIONS
==================

IMMEDIATE (This Week):
- [Action based on current metrics]
- [Action based on current metrics]

SHORT-TERM (This Month):
- [Action based on current metrics]
- [Action based on current metrics]

STRATEGIC (This Quarter):
- [Action based on current metrics]
- [Action based on current metrics]
```

Examples of context-aware recommendations:

**If runway <6 months:**
- 🚨 URGENT: Begin fundraising immediately or implement emergency burn reduction
- Schedule board meeting to discuss bridge financing options
- Model 30-50% burn reduction scenarios

**If burn multiple >3x:**
- ⚠️ Reduce customer acquisition costs or improve revenue per customer
- Analyze marketing channel ROI and cut underperforming spend
- Consider raising prices or improving conversion rates

**If revenue growth <5% MoM:**
- 📈 Focus on growth initiatives - current trajectory won't support burn rate
- Review sales pipeline and conversion funnel
- Consider product-market fit adjustments

**If LTV:CAC <2:1:**
- 💰 Improve unit economics before scaling further
- Reduce churn to increase LTV
- Optimize CAC through better targeting or cheaper channels

## Output Format

```
═══════════════════════════════════════════════════════════
FINANCIAL SNAPSHOT
As of: [Today's Date and Time]
Data Source: Mercury Bank
═══════════════════════════════════════════════════════════

📊 EXECUTIVE SUMMARY
─────────────────────────────────────────────────────────
Health Score: XX/100 🟢/🟡/🟠/🔴
Status: [One-line assessment]
Key Alert: [Most critical issue if any]

💰 CASH POSITION
─────────────────────────────────────────────────────────
Current Balance: $XXX,XXX
Monthly Burn: $XX,XXX
Runway: X.X months (until [Date])

📈 REVENUE & GROWTH
─────────────────────────────────────────────────────────
MRR: $XX,XXX (+X.X% MoM)
ARR: $XXX,XXX
Revenue Covers: XX% of burn

🎯 EFFICIENCY METRICS
─────────────────────────────────────────────────────────
Burn Multiple: X.Xx
LTV:CAC Ratio: X.X:1
Gross Margin: XX%

💸 BURN BREAKDOWN
─────────────────────────────────────────────────────────
[Category breakdown with percentages]

📉 12-MONTH FORECAST
─────────────────────────────────────────────────────────
[Projection table or summary]
Path to Profitability: XX months

⚡ RECOMMENDED ACTIONS
─────────────────────────────────────────────────────────
IMMEDIATE:
- [Action 1]
- [Action 2]

SHORT-TERM:
- [Action 1]
- [Action 2]

═══════════════════════════════════════════════════════════
```

## Alerts and Warnings

**🚨 CRITICAL ALERTS**:
- Runway <3 months: Emergency measures required
- Burn increasing >30% without revenue growth
- Burn multiple >5x: Unsustainable capital efficiency
- Negative cash flow with no clear path to profitability

**⚠️ WARNING SIGNS**:
- Runway <6 months: Begin fundraising immediately
- Revenue growth <5% for 3+ months
- Burn increasing for 3+ consecutive months
- Single expense category >60% of total burn

**ℹ️ MONITORING**:
- Runway <12 months: Plan fundraising timeline
- Burn multiple >2x: Monitor efficiency
- Customer concentration risk (one customer >25% revenue)

## Integration Points

This command combines data from:
- `/burn-rate` - Monthly operating expenses
- `/runway` - Cash runway calculations
- Mercury MCP - Real-time balance and transactions
- Manual input (if needed) - Revenue, customer metrics

## Related Commands

After reviewing financial snapshot:
- `/burn-rate [period]` - Deep dive into burn analysis
- `/runway` - Detailed runway scenarios and fundraising guidance
- `/cost-optimization` - If efficiency needs improvement (expense-management plugin)

## Automated Monitoring with Agents

For continuous financial monitoring, use both agents together:

### runway-monitor Agent

**When to use:**
- After your first financial snapshot
- Critical when runway <12 months
- Set up daily monitoring (9 AM recommended)

**How to invoke:**
```
Use the runway-monitor agent to track my cash runway daily
```

**What it monitors:**
- Daily cash balance changes
- Runway threshold crossings (12mo, 9mo, 6mo, 3mo)
- Fundraising timeline tracking
- Unexpected burn spikes

### burn-analyzer Agent

**When to use:**
- Weekly spending analysis
- Before board meetings
- When looking for cost savings
- After financial snapshot shows concerning trends

**How to invoke:**
```
Use the burn-analyzer agent to analyze spending patterns and find optimization opportunities
```

**What it analyzes:**
- Transaction categorization
- Spending anomalies and duplicates
- Cost optimization opportunities
- Efficiency metrics and trends

**Recommended Setup:**
- runway-monitor: Daily (proactive runway alerts)
- burn-analyzer: Weekly (deep cost analysis)
- financial-snapshot: Weekly/bi-weekly (comprehensive review)

## Refresh Frequency

**Recommended cadence**:
- Weekly: During critical periods (runway <6mo, rapid growth)
- Bi-weekly: During normal operations
- Monthly: Stable, healthy metrics

Agents handle continuous monitoring between snapshot reviews.

## Data Requirements

**Minimum Required**:
- Mercury Bank connection (for cash balance and expenses)
- Current revenue/MRR (from Mercury or manual input)

**Optional for Enhanced Insights**:
- Customer count and churn rate
- Sales pipeline data
- Budget/forecast data
- Prior period comparisons

## Example Output

```
═══════════════════════════════════════════════════════════
FINANCIAL SNAPSHOT
As of: February 7, 2026 at 2:45 PM PST
Data Source: Mercury Bank
═══════════════════════════════════════════════════════════

📊 EXECUTIVE SUMMARY
─────────────────────────────────────────────────────────
Health Score: 72/100 🟡
Status: Good financial health with moderate growth
Key Alert: Runway at 8.5 months - plan fundraising timeline

💰 CASH POSITION
─────────────────────────────────────────────────────────
Current Balance: $638,500
Monthly Burn: $75,200
Runway: 8.5 months (until October 15, 2026)

📈 REVENUE & GROWTH
─────────────────────────────────────────────────────────
MRR: $42,300 (+8.2% MoM)
ARR: $507,600
Revenue Covers: 56% of burn

🎯 EFFICIENCY METRICS
─────────────────────────────────────────────────────────
Burn Multiple: 2.1x (Good)
LTV:CAC Ratio: 3.2:1 (Healthy)
Gross Margin: 78%

💸 BURN BREAKDOWN
─────────────────────────────────────────────────────────
Payroll & Benefits:        $48,500 (64%)
Engineering/Infrastructure: $12,800 (17%)
Sales & Marketing:          $9,200 (12%)
General & Admin:            $4,700 (6%)

📉 12-MONTH FORECAST
─────────────────────────────────────────────────────────
At 8% monthly revenue growth:
- Profitability: November 2026 (9 months)
- Current runway sufficient to reach profitability
- Assumes burn stays flat at $75K/month

⚡ RECOMMENDED ACTIONS
─────────────────────────────────────────────────────────
IMMEDIATE:
- Monitor burn closely - keep at or below $75K/month
- Focus on maintaining 8%+ MoM revenue growth

SHORT-TERM:
- Begin exploring fundraising options for Q3 2026
- Target $1.5M-$2M raise to extend runway to 18-24 months
- Prepare investor materials and update financial model

STRATEGIC:
- Path to profitability is achievable - prioritize growth
- Consider modest burn reduction ($10K-15K/mo) to extend runway
- Build 3-6 month cash buffer beyond profitability date

═══════════════════════════════════════════════════════════
```
