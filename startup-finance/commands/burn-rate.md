---
description: Calculate monthly burn rate from Mercury Bank transactions
argument-hint: "[period]"
---

# Burn Rate Calculator

Calculate your startup's monthly cash burn rate using actual Mercury Bank transaction data.

## Usage

```
/burn-rate [period]
```

### Arguments

- `period` — Optional. Time period to analyze (default: last 3 months)
  - `1m` or `30d` — Last 30 days
  - `3m` or `90d` — Last 3 months (recommended for accuracy)
  - `6m` — Last 6 months
  - `ytd` — Year to date
  - Specific month: `2024-12` or `dec-2024`

## Workflow

### 1. Fetch Transaction Data from Mercury

Use the Mercury MCP server to pull transaction history:
- Get all transactions for the specified period
- Filter to expense transactions (debits, excluding transfers)
- Exclude one-time items if calculating ongoing burn

If Mercury MCP is not connected:
> Connect the Mercury MCP server to automatically fetch transaction data. Without it, you'll need to manually provide expense data.

### 2. Categorize Expenses

Categorize all expense transactions:

**Operating Expenses** (include in burn rate):
- Payroll and benefits
- Contractor payments
- SaaS subscriptions (AWS, Vercel, Stripe, etc.)
- Marketing and advertising spend
- Office expenses
- Professional services (legal, accounting)
- Software and tools
- Insurance

**Exclude from Burn Rate**:
- One-time capital expenses
- Equity purchases
- Loan repayments (principal)
- Transfers between accounts
- Refunds or reimbursements

### 3. Calculate Monthly Burn Rate

```
Total Operating Expenses for Period: $XXX,XXX
Number of Months in Period: X
Monthly Burn Rate: $XX,XXX/month
```

If period is less than a full month, annualize appropriately.

### 4. Analyze Burn Components

Break down burn by category to understand where cash is going:

| Category | Amount | % of Burn | Trend |
|----------|--------|-----------|-------|
| Payroll & Benefits | $XX,XXX | XX% | ↑ |
| Engineering/Infrastructure | $XX,XXX | XX% | → |
| Marketing & Sales | $XX,XXX | XX% | ↓ |
| G&A (General & Admin) | $XX,XXX | XX% | → |
| **Total Burn** | **$XX,XXX** | **100%** | |

### 5. Trend Analysis

Compare to prior periods:

```
Current Month:     $XX,XXX/month
Prior Month:       $XX,XXX/month
3-Month Average:   $XX,XXX/month
6-Month Average:   $XX,XXX/month

Month-over-Month Change: +/- $X,XXX (+/- X.X%)
Trend: Increasing / Stable / Decreasing
```

### 6. Key Metrics

Calculate related efficiency metrics:

**Burn Multiple**:
```
Burn Multiple = Net Burn / Net New ARR
(How many dollars you burn to add $1 of ARR)
Target: <1.5x (efficient), 1.5-3x (acceptable), >3x (inefficient)
```

**Months to Default** (covered in `/runway` command):
```
Runway = Current Cash Balance / Monthly Burn Rate
```

**Revenue as % of Burn**:
```
If monthly revenue = $XX,XXX and burn = $XX,XXX
Revenue covers XX% of burn
Path to profitability: Need to grow revenue by $XX,XXX or reduce burn by $XX,XXX
```

### 7. Alerts and Recommendations

Flag concerning patterns:

**🚨 High Priority Alerts**:
- Burn increasing >20% month-over-month without revenue growth
- Burn multiple >3x (burning too much per dollar of ARR added)
- Any single category >50% of total burn (concentration risk)

**⚠️ Medium Priority Alerts**:
- Burn increasing for 3+ consecutive months
- Burn multiple 2-3x
- Runway <6 months at current burn rate

**Recommendations**:
- If burn is increasing: Identify which categories are growing and why
- If burn multiple is high: Focus on revenue growth or cost optimization
- If specific category dominates: Evaluate if spending is efficient

## Output Format

Present results in this structure:

```
BURN RATE ANALYSIS
Period: [Date range]
Data Source: Mercury Bank

SUMMARY
==================
Monthly Burn Rate: $XX,XXX/month
Prior Period: $XX,XXX/month
Change: +/- $X,XXX (+/- X.X%)

BURN BREAKDOWN
==================
[Category breakdown table]

EFFICIENCY METRICS
==================
Burn Multiple: X.Xx
Revenue as % of Burn: XX%
Months to Profitability: XX months (at current growth rate)

TREND
==================
[Trend chart or description]

ALERTS
==================
[Any flags or recommendations]
```

## Next Steps

After reviewing burn rate, suggest:
- Run `/runway` to see how burn impacts cash runway
- Run `/financial-snapshot` for complete financial picture
- If burn is concerning, run `/cost-optimization` to identify savings (expense-management plugin)

## Continuous Analysis with Agents

For deep burn pattern analysis, use the **burn-analyzer agent**:

**When to use:**
- After running this command, invoke the agent for weekly analysis
- When burn is increasing unexpectedly
- Before board meetings or financial reviews
- When looking for cost optimization opportunities

**How to invoke:**
```
Use the burn-analyzer agent to analyze my spending patterns and find optimization opportunities
```

**What it does:**
- Categorizes all Mercury transactions automatically
- Detects spending anomalies and outliers
- Identifies cost optimization opportunities (SaaS, infrastructure, vendors)
- Tracks burn efficiency metrics over time
- Flags duplicate charges and billing errors

**Benefits:**
- Find $5K-$20K/month in savings automatically
- Catch billing errors within 24 hours
- Understand where every dollar is going
- Improve burn multiple and capital efficiency
