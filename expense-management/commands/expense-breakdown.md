---
description: Comprehensive breakdown of expenses by category with trends and analysis
argument-hint: "[period]"
---

# Expense Breakdown

Get a detailed breakdown of all expenses by category, with automatic categorization, trend analysis, and spend patterns.

## Usage

```
/expense-breakdown [period]
```

### Arguments

- `period` — Optional. Time period to analyze (default: last 30 days)
  - `7d` — Last 7 days
  - `30d` or `1m` — Last 30 days (default)
  - `90d` or `3m` — Last 3 months
  - `ytd` — Year to date
  - Specific month: `2026-01` or `jan-2026`

## Workflow

### 1. Fetch Transactions from Mercury

Use Mercury MCP to pull all transactions for the period:
- Get all debit transactions (expenses)
- Include pending transactions if analyzing current month
- Exclude transfers between your own accounts
- Include refunds (net against original category)

If Mercury MCP is not connected:
> Connect Mercury MCP server for automatic expense tracking. Manual expense entry is not recommended.

### 2. Auto-Categorize Transactions

Apply intelligent categorization to each transaction:

**Category Assignment Logic**:

```
1. Check vendor name against known patterns:
   - "AWS" or "Amazon Web Services" → Engineering/Infrastructure
   - "Gusto" or "ADP" or "Rippling" → Payroll
   - "Google Ads" or "Meta" or "LinkedIn Ads" → Marketing
   - Pattern matching for common SaaS vendors

2. Check transaction description:
   - Contains "payroll" → Payroll
   - Contains "insurance" → G&A
   - Contains "legal" or "attorney" → Legal (G&A)

3. Check amount patterns:
   - Large recurring amount (e.g., $40K biweekly) → Likely payroll
   - Small recurring amounts (<$500) → Likely SaaS subscriptions
   - Very large one-time (>$10K) → Flag for manual review

4. Machine learning (if available):
   - Learn from past categorizations
   - Suggest categories for new vendors
```

**Standard Categories**:

**Personnel**:
- Payroll (salaries, wages)
- Benefits (health insurance, 401k)
- Contractors
- Recruiting

**Engineering & Infrastructure**:
- Cloud hosting (AWS, GCP, Azure)
- Development tools (GitHub, Vercel, Render)
- API costs (Stripe, Twilio, SendGrid)
- Database and storage
- Security tools

**Sales & Marketing**:
- Advertising (Google, Meta, LinkedIn)
- Marketing tools (HubSpot, Mailchimp)
- Events and conferences
- Content and agencies
- Sales tools (CRM, outreach)

**General & Administrative**:
- Legal and accounting
- Insurance
- Office expenses and rent
- Business software (Slack, Zoom, Notion)
- Bank fees
- Travel

**Uncategorized**:
- Transactions that don't match known patterns
- New vendors requiring manual categorization

### 3. Calculate Category Totals

Aggregate spending by category:

```
EXPENSE BREAKDOWN (Last 30 Days)
Period: Jan 8 - Feb 7, 2026
Total Spend: $XX,XXX
────────────────────────────────────────

PERSONNEL: $XX,XXX (XX%)
├─ Payroll: $XX,XXX
├─ Benefits: $X,XXX
├─ Contractors: $X,XXX
└─ Recruiting: $XXX

ENGINEERING & INFRASTRUCTURE: $XX,XXX (XX%)
├─ AWS: $X,XXX
├─ Development Tools: $X,XXX
├─ API Costs: $XXX
└─ Other: $XXX

SALES & MARKETING: $X,XXX (XX%)
├─ Advertising: $X,XXX
├─ Marketing Tools: $XXX
├─ Events: $XXX
└─ Other: $XXX

GENERAL & ADMINISTRATIVE: $X,XXX (XX%)
├─ Legal & Accounting: $X,XXX
├─ Insurance: $XXX
├─ Office: $XXX
└─ Other: $XXX

UNCATEGORIZED: $XXX (X%)
└─ [List of uncategorized transactions for manual review]
```

### 4. Trend Analysis

Compare current period to prior periods:

```
SPENDING TRENDS
────────────────────────────────────────
Category               Current    Prior    Change
────────────────────────────────────────
Personnel              $48,500   $45,200   +7.3% ↑
Eng/Infrastructure     $12,800   $11,900   +7.6% ↑
Sales & Marketing       $9,200    $8,100  +13.6% ↑
G&A                     $4,700    $4,500   +4.4% →
────────────────────────────────────────
TOTAL                  $75,200   $69,700   +7.9% ↑

Key Drivers:
• Personnel: New contractor started ($3,500/mo)
• Marketing: Increased Google Ads budget (+$1,200)
• Infrastructure: AWS spike due to traffic growth (+$900)
```

### 5. Vendor Analysis

Show top vendors by spend:

```
TOP 10 VENDORS (Last 30 Days)
────────────────────────────────────────
1. Gusto (Payroll)                 $42,500
2. AWS (Infrastructure)              $2,800
3. Google Ads (Marketing)            $4,200
4. Office Rent (G&A)                 $3,500
5. Deel (Contractors)                $3,500
6. GitHub (Development)              $1,200
7. LinkedIn Ads (Marketing)          $2,800
8. Vercel (Infrastructure)           $1,100
9. Wilson Sonsini (Legal)            $2,500
10. Notion (G&A)                       $800
────────────────────────────────────────
Top 10 Total: $65,900 (88% of spend)
```

### 6. Recurring vs One-Time

Identify spending patterns:

```
SPENDING PATTERNS
────────────────────────────────────────
Recurring (Monthly): $68,500 (91%)
├─ Payroll: $42,500
├─ SaaS Subscriptions: $12,800
├─ Office Rent: $3,500
└─ Other: $9,700

One-Time/Variable: $6,700 (9%)
├─ Legal fees: $2,500
├─ Conference ticket: $1,500
├─ Contractor (one-off): $1,200
└─ Other: $1,500
────────────────────────────────────────

Recurring spend is predictable and manageable.
One-time costs are within normal range (<15% is healthy).
```

### 7. Per-Unit Metrics

Calculate efficiency metrics:

```
PER-UNIT SPEND ANALYSIS
────────────────────────────────────────
Total Spend: $75,200
Employees: 8 FTEs
Customers: 42
MRR: $25,000

Metrics:
• Spend per Employee: $9,400/month
• Spend per Customer: $1,790/month
• Spend per $1 MRR: $3.01
• Infrastructure per Customer: $305/month
• CAC (Marketing): $219/customer

Benchmarks:
• Spend/Employee: $9.4K vs $20-30K industry (efficient ✅)
• Spend/MRR: $3 vs $1.50-2.50 target (high ⚠️)
```

### 8. Category Deep Dive

Allow drilling into specific categories:

```
Request: "Show me all Engineering & Infrastructure expenses"

ENGINEERING & INFRASTRUCTURE BREAKDOWN
────────────────────────────────────────
Total: $12,800 (17% of total spend)
Trend: +7.6% vs prior month

Detailed Breakdown:
────────────────────────────────────────
Cloud Hosting: $3,900 (30%)
├─ AWS: $2,800
│  ├─ EC2: $1,680
│  ├─ RDS: $560
│  ├─ S3: $280
│  └─ Other: $280
└─ Vercel: $1,100

Development Tools: $4,200 (33%)
├─ GitHub: $1,200
├─ Datadog: $1,500
├─ Sentry: $800
└─ Other: $700

API Costs: $2,400 (19%)
├─ Stripe: $1,200 (payment processing)
├─ Twilio: $800 (SMS/voice)
└─ SendGrid: $400 (email)

Other Infrastructure: $2,300 (18%)
├─ CloudFlare: $500
├─ PlanetScale: $900
└─ Other: $900

Cost Drivers:
• AWS increased due to 40% traffic growth (expected)
• Datadog added new monitors (planned expansion)
• Stripe fees grew with revenue (good signal)

Optimization Opportunities:
• AWS reserved instances: save $840/month
• Consolidate monitoring (Datadog + Sentry → Datadog): save $400/month
```

## Output Format

```
═══════════════════════════════════════════════════════════
EXPENSE BREAKDOWN
Period: [Date Range]
Total Spend: $XX,XXX
Data Source: Mercury Bank
═══════════════════════════════════════════════════════════

📊 CATEGORY SUMMARY
─────────────────────────────────────────────────────────
[Category breakdown with percentages]

📈 TRENDS (vs Prior Period)
─────────────────────────────────────────────────────────
[Category trend table with changes]

🏢 TOP VENDORS
─────────────────────────────────────────────────────────
[Top 10 vendors by spend]

🔄 SPENDING PATTERNS
─────────────────────────────────────────────────────────
Recurring: $XX,XXX (XX%)
One-Time: $X,XXX (X%)

📉 PER-UNIT METRICS
─────────────────────────────────────────────────────────
[Efficiency metrics]

⚠️ ATTENTION NEEDED
─────────────────────────────────────────────────────────
[Uncategorized transactions or anomalies]

═══════════════════════════════════════════════════════════
```

## Use Cases

**Monthly Financial Reviews**:
- "Show me last month's expense breakdown"
- Review category spending vs budget
- Identify trends and anomalies

**Budget Planning**:
- "What did we spend on engineering in Q1?"
- Use historical data to forecast future spend
- Set realistic budgets by category

**Cost Investigation**:
- "Why did marketing spend increase 30%?"
- Drill into specific categories
- Identify specific transactions driving changes

**Board Reporting**:
- "Give me expense breakdown for the quarter"
- High-level category view for board deck
- Show spend efficiency metrics

## Related Commands

- `/budget-variance` - Compare actual spend vs budget by category
- `/cost-optimization` - Find specific savings opportunities based on expense patterns
- `/anomaly-report` - Flag unusual transactions for review
- `/burn-rate` - See how expense breakdown contributes to overall burn (startup-finance plugin)

## Notes

**Categorization Accuracy**:
- Auto-categorization is ~95% accurate for known vendors
- Review uncategorized transactions monthly to improve accuracy
- Manually categorize new vendors to build the learning model

**Integration with Budgets**:
- This command shows actual spending
- Use `/budget-variance` to compare against budgeted amounts
- Budget tracking requires setting category budgets (one-time setup)

**Data Freshness**:
- Mercury data updates in real-time
- Pending transactions are included in current period analysis
- Historical data is final and won't change
