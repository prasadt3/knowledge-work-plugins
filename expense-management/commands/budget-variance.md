---
description: Compare actual expenses vs budget by category and flag variances
argument-hint: "[period]"
---

# Budget Variance Analysis

Track actual spending against your budget by category, identify variances, and understand where you're over or under budget.

## Usage

```
/budget-variance [period]
```

### Arguments

- `period` — Optional. Time period to analyze (default: current month)
  - `current` or `mtd` — Month-to-date (default)
  - `last-month` — Previous month
  - `q1`, `q2`, `q3`, `q4` — Specific quarter
  - `ytd` — Year to date
  - Specific month: `2026-01` or `jan-2026`

## Workflow

### 1. Load Budget

Retrieve budget for the specified period:

**Budget Source Options**:

**Option A: Stored Budget** (recommended):
- Budget defined in configuration file or database
- Monthly budget by category
- Can be different for each month (seasonal adjustments)

**Option B: Manual Input** (first-time setup):
> No budget found for this period. Please provide monthly budgets by category, or I can suggest based on historical spend patterns.

**Example Budget Setup**:
```json
{
  "monthly_budget": {
    "personnel": 50000,
    "engineering_infrastructure": 15000,
    "sales_marketing": 12000,
    "general_admin": 6000,
    "total": 83000
  }
}
```

**Option C: Auto-Suggest from Historical Data**:
```
Suggested Budget (based on last 3 months average):
• Personnel: $48,500/month
• Engineering & Infrastructure: $12,500/month
• Sales & Marketing: $10,000/month
• G&A: $5,000/month
───────────────────────────────
Total: $76,000/month

Approve this budget or provide custom amounts?
```

### 2. Fetch Actual Expenses

Use Mercury MCP to get actual spending:
- Pull transactions for the period
- Auto-categorize using expense-breakdown logic
- Calculate totals by category

### 3. Calculate Variances

For each category, calculate:

```
Variance = Actual - Budget
Variance % = (Variance / Budget) × 100%

Example:
Budget: $50,000
Actual: $54,200
Variance: +$4,200 (+8.4% over budget)
```

**Variance Interpretation**:
- **Over Budget** (positive variance): Spending more than planned
- **Under Budget** (negative variance): Spending less than planned
- **On Budget** (±5% variance): Within acceptable range

### 4. Categorize Variance Severity

Flag variances by severity:

**🔴 Critical** (>20% variance):
- Requires immediate attention
- Significant budget overrun or underutilization
- May indicate budgeting error or major unplanned expense

**🟡 Warning** (10-20% variance):
- Monitor closely
- May need adjustment next period
- Could be normal variation or trend starting

**🟢 Normal** (<10% variance):
- Within acceptable range
- No action needed
- Budget is accurate

### 5. Identify Variance Drivers

For each over-budget category, identify root causes:

```
CATEGORY: Engineering & Infrastructure
Budget: $15,000
Actual: $18,500
Variance: +$3,500 (+23.3%) 🔴 CRITICAL

Top Drivers of Overage:
1. AWS: +$2,100 over expected
   - Expected: $2,800, Actual: $4,900
   - Root cause: Traffic spike (40% growth), new dev environments

2. Datadog: +$800 over expected
   - Expected: $1,200, Actual: $2,000
   - Root cause: Added APM monitoring for new services

3. New vendor (CloudFlare Enterprise): +$600
   - Not in budget
   - Root cause: Unplanned upgrade for DDoS protection

Recommendation:
• AWS: Expected for growth, adjust budget to $4,500/month
• Datadog: Planned expansion, update budget
• CloudFlare: One-time decision, add to ongoing budget
• New Monthly Budget: $18,000 (from $15,000)
```

### 6. Year-to-Date Tracking

Show cumulative variance YTD:

```
YEAR-TO-DATE VARIANCE (Jan-Feb 2026)
────────────────────────────────────────

Category                  Budget      Actual    Variance    Status
──────────────────────────────────────────────────────────────────
Personnel               $100,000    $96,700    -$3,300 ✅  (-3.3%)
Eng/Infrastructure       $30,000    $31,300    +$1,300 ⚠️  (+4.3%)
Sales & Marketing        $24,000    $27,600    +$3,600 🔴 (+15.0%)
G&A                      $12,000    $11,200      -$800 ✅  (-6.7%)
──────────────────────────────────────────────────────────────────
TOTAL                   $166,000   $166,800      +$800    (+0.5%)

Overall Status: 🟢 On Track
- Total spend within 1% of budget
- Marketing overage offset by personnel savings
- Infrastructure variance minor and expected
```

### 7. Forecast to End of Period

Project spend for rest of month/quarter:

```
MONTH-TO-DATE + FORECAST (February 2026)
────────────────────────────────────────

Today: Feb 15 (50% through month)

Category              Budget    MTD Actual   Pace      Forecast    Variance
──────────────────────────────────────────────────────────────────────────
Personnel            $50,000      $25,000   On pace    $50,000         $0 ✅
Eng/Infrastructure   $15,000       $9,200   123% pace  $18,400    +$3,400 🔴
Sales & Marketing    $12,000       $4,500    75% pace   $9,000    -$3,000 ⚠️
G&A                   $6,000       $2,800    93% pace   $5,600      -$400 ✅
──────────────────────────────────────────────────────────────────────────
TOTAL                $83,000      $41,500   On pace    $83,000         $0

Forecast Logic:
• Personnel: Biweekly payroll, 2nd payroll on Feb 28 = right on budget
• Infrastructure: Running 23% over pace, forecast overrun
• Marketing: Underspending, may have campaigns planned for month-end
• G&A: Tracking normally

Recommended Actions:
• Infrastructure: Investigate AWS spike, confirm it's expected growth
• Marketing: Confirm campaigns on schedule or reduce budget forecast
```

### 8. Budget vs Actuals Trend

Show monthly trend over time:

```
MONTHLY BUDGET VARIANCE TREND (Last 6 Months)
────────────────────────────────────────────

         Sep    Oct    Nov    Dec    Jan    Feb
Budget   $72K   $74K   $76K   $78K   $80K   $83K
Actual   $69K   $71K   $79K   $81K   $82K   $83K*
Variance -$3K   -$3K   +$3K   +$3K   +$2K    $0*
Status    ✅     ✅     ⚠️     ⚠️     ✅     ✅

*February forecast

Observations:
• Budgets increasing 3-5% monthly (planned hiring growth)
• Nov-Dec: Over budget due to year-end hiring
• Jan-Feb: Back on track
• Trend: Improving budget accuracy
```

## Output Format

```
═══════════════════════════════════════════════════════════
BUDGET VARIANCE ANALYSIS
Period: [Date Range]
Budget: $XX,XXX | Actual: $XX,XXX | Variance: $X,XXX (X%)
═══════════════════════════════════════════════════════════

📊 VARIANCE SUMMARY
─────────────────────────────────────────────────────────
Category                Budget      Actual    Variance     Status
────────────────────────────────────────────────────────────────
[Category rows with color-coded status]

Overall Status: 🟢/🟡/🔴

📈 VARIANCE DRIVERS
─────────────────────────────────────────────────────────
[For over-budget categories]:

🔴 [CATEGORY NAME] (+XX% over)
Top Drivers:
1. [Driver 1]: +$X,XXX
2. [Driver 2]: +$XXX
3. [Driver 3]: +$XXX

Recommendation: [Action]

📉 YEAR-TO-DATE TRACKING
─────────────────────────────────────────────────────────
[Cumulative variance table]

🔮 FORECAST (If MTD)
─────────────────────────────────────────────────────────
[Projected end-of-period spend vs budget]

⚡ RECOMMENDED ACTIONS
─────────────────────────────────────────────────────────
IMMEDIATE:
- [Action 1]

THIS MONTH:
- [Action 2]

NEXT BUDGET CYCLE:
- [Budget adjustment recommendations]

═══════════════════════════════════════════════════════════
```

## Budget Adjustment Workflow

When variances persist, update budgets:

```
BUDGET ADJUSTMENT RECOMMENDATIONS
────────────────────────────────────────

Current Issue: Engineering & Infrastructure consistently over budget
- Jan: +15% over
- Feb: +23% over
- Root cause: Business growth (40% traffic increase)

Options:

Option 1: Increase Budget (Recommended)
- Current: $15,000/month
- Recommended: $18,000/month (+20%)
- Justification: Growth-driven, infrastructure scales with customers
- Impact on total budget: $83K → $86K/month

Option 2: Optimize Spend
- Reduce costs through reserved instances: -$840/month
- Right-size over-provisioned resources: -$500/month
- Total savings: -$1,340/month
- Keep budget at $15,000

Option 3: Combination
- Increase budget to $16,500
- Implement optimizations for -$1,340
- Net: $15,160 actual spend (on budget)

Recommendation: Option 1
- Infrastructure costs are growth indicators (good thing!)
- Optimizations should happen regardless
- Update budget to reflect new baseline
```

## Use Cases

**Monthly Financial Close**:
- "Show budget variance for last month"
- Review actuals vs budget
- Prepare board report on spending

**In-Month Monitoring**:
- "Am I on track this month?"
- Check MTD spend vs pace
- Forecast month-end position

**Budget Planning**:
- "Show YTD variance to inform next quarter's budget"
- Identify consistent over/under spend
- Adjust future budgets based on trends

**Variance Investigation**:
- "Why am I over budget on marketing?"
- Drill into specific drivers
- Determine if variance is one-time or recurring

## Alerts

**🔴 Critical Alerts**:
- Any category >30% over budget
- Total budget overrun >15%
- Consistent overruns 3+ months

**🟡 Warning Alerts**:
- Category 15-30% over budget
- Total budget 10-15% over
- Trending toward overrun (pace analysis)

**ℹ️ Informational**:
- Category <10% variance (normal)
- Significant under-spend (>20% under) - may indicate missed initiatives

## Integration with Other Commands

- `/expense-breakdown` - Get actual spending details used in variance analysis
- `/cost-optimization` - Find ways to reduce spend in over-budget categories
- `/burn-rate` - Overall burn calculation (may differ from budget if actuals vary)

## Budget Setup (First Time)

If no budget exists, command will guide through setup:

```
No budget found. Let's set up your monthly budget.

I can suggest a budget based on your last 3 months of spending:

Suggested Monthly Budget:
• Personnel: $48,500 (avg of last 3 months)
• Engineering & Infrastructure: $12,500
• Sales & Marketing: $10,000
• General & Admin: $5,000
───────────────────────────────
Total: $76,000/month

Options:
1. Accept suggested budget
2. Adjust categories (provide custom amounts)
3. Set growth-adjusted budget (e.g., +10% monthly)

Which would you like?
```

## Notes

**Budget Philosophy**:
- Budgets should be realistic, not aspirational
- 10-15% variance is normal for early-stage startups
- Update budgets quarterly based on trends
- Don't penalize growth-driven spending

**Variance Context Matters**:
- Over budget on marketing with strong CAC ROI? Good variance.
- Over budget on G&A with no clear driver? Bad variance.
- Under budget on hiring due to delays? May hurt product velocity.

**Budget as a Tool**:
- Budgets help with planning and control, not restriction
- Variance analysis identifies trends and anomalies
- Use it to make informed decisions, not to limit spending arbitrarily
