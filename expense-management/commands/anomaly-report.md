---
description: Detect unusual transactions, duplicates, and spending anomalies requiring review
argument-hint: "[period]"
---

# Anomaly Report

Automatically detect unusual transactions, duplicate charges, spending spikes, and other financial anomalies that require attention.

## Usage

```
/anomaly-report [period]
```

### Arguments

- `period` — Optional. Time period to analyze (default: last 30 days)
  - `7d` — Last 7 days (for quick checks)
  - `30d` or `1m` — Last 30 days (default)
  - `90d` — Last 3 months (comprehensive)
  - `today` — Today's transactions only

## Workflow

### 1. Fetch Transactions

Pull all Mercury transactions for the period:
- All debit transactions (expenses)
- Include pending transactions
- Get historical data for comparison (last 90 days minimum)

### 2. Anomaly Detection Algorithms

Run multiple detection algorithms:

#### A. Statistical Outliers

For each vendor, identify transactions significantly above normal:

```
Algorithm: Z-Score (Standard Deviation)

For vendor "AWS":
  Historical transactions: $2,500, $2,700, $2,850, $2,600, $2,750
  Mean: $2,680
  Standard Deviation: $134

  Today's transaction: $5,200
  Z-Score: (5200 - 2680) / 134 = 18.8σ

  If Z-Score > 3: FLAG AS ANOMALY
```

**Example Detection**:
```
🚩 STATISTICAL ANOMALY: AWS

Transaction: $5,200 on Feb 7, 2026
Expected range: $2,400-$3,000 (based on last 90 days)
Deviation: +$2,520 (+94% above average)
Severity: 🔴 Critical (>3σ)

Possible Causes:
• Unexpected traffic spike (check CloudWatch)
• New service/instance launched
• Configuration error (runaway compute)
• Billing error from AWS

Action Required: Investigate immediately
```

#### B. Duplicate Detection

Identify potential duplicate charges:

```
Algorithm: Same Vendor + Similar Amount + Close Timing

Rules:
- Same vendor name
- Amount within ±10% OR exact match
- Within 7 days
- Not a recurring scheduled payment

Example:
  Stripe: $1,245 on Feb 5, 2026
  Stripe: $1,245 on Feb 6, 2026
  → FLAG AS POTENTIAL DUPLICATE
```

**Example Detection**:
```
🚩 POTENTIAL DUPLICATE: Stripe

Charge 1: $1,245.00 on Feb 5, 2026 3:42 PM
Charge 2: $1,245.00 on Feb 6, 2026 9:15 AM
Time difference: 18 hours
Amount: Exact match

Status: Needs Review
Action: Verify with Stripe dashboard if two separate billing cycles or error
```

#### C. Frequency Anomalies

Detect unexpected charging frequency:

```
Algorithm: Frequency Pattern Matching

For "Notion" (normally monthly):
  Expected: 1 charge per 30 days
  Actual: 2 charges in 5 days
  → FLAG AS FREQUENCY ANOMALY
```

**Example Detection**:
```
🚩 FREQUENCY ANOMALY: Notion

Expected: Monthly charge (~$200 on 15th of month)
Detected:
  - $200 on Feb 3, 2026
  - $200 on Feb 15, 2026 (expected)

Total: 2 charges this month (normally 1)

Possible Causes:
• Accidental double billing
• Plan change or upgrade
• Catch-up charge from previous month
• Manual charge by vendor

Action Required: Contact Notion support to verify
```

#### D. New Large Vendors

Flag first-time large expenses:

```
Algorithm: New Vendor Detection

Rules:
- Vendor not seen in last 180 days
- Amount > $1,000
- Not categorized as "expected" (e.g., new hire payroll)
```

**Example Detection**:
```
🚩 NEW LARGE VENDOR: Salesforce

Transaction: $3,500 on Feb 5, 2026
Status: First charge from this vendor
Category: Sales & Marketing (auto-categorized)

Context:
• No prior charges from Salesforce in history
• Amount exceeds $1K threshold
• May be legitimate (new CRM adoption)

Action Required: Confirm this was an authorized purchase
```

#### E. Price Increase Detection

Identify vendors who increased pricing:

```
Algorithm: Recurring Charge Price Change

For vendors with monthly recurring charges:
  Previous charge: $X
  Current charge: $X + ΔX
  If ΔX > 10%: FLAG AS PRICE INCREASE
```

**Example Detection**:
```
🚩 PRICE INCREASE: HubSpot

Previous charge: $800/month (last 6 months)
Current charge: $960/month
Increase: +$160 (+20%)

Status: Unexpected price increase

Possible Causes:
• Plan auto-upgrade (more contacts added)
• Renewal at higher rate
• Added features/seats
• Vendor price increase

Action Required:
1. Review HubSpot account for plan changes
2. Check if contacts increased triggering tier change
3. Consider renegotiation if unilateral increase
```

#### F. Weekend/Holiday Charges

Flag unusual timing:

```
Algorithm: Unusual Timing Detection

Rules:
- Charges on Saturday/Sunday (when most vendors don't bill)
- Charges on holidays
- Charges outside business hours (for B2B vendors)
- Exempt: AWS and other 24/7 services
```

**Example Detection**:
```
🚩 UNUSUAL TIMING: Wilson Sonsini (Legal)

Transaction: $4,500 on Sunday, Feb 9, 2026 at 2:37 AM
Type: Legal services (normally M-F business hours)

Status: Highly unusual

Possible Issues:
• Billing system error (wrong date/time)
• Manual charge with incorrect timestamp
• Fraudulent charge (if not authorized)

Action Required: Contact Wilson Sonsini billing immediately
```

#### G. Amount Pattern Anomalies

Detect unusual amount patterns:

```
Algorithm: Round Number Detection

Legitimate charges are rarely round numbers:
  Suspicious: $5,000.00 exactly
  Legitimate: $4,847.32 (typical invoice)

Also flag:
- All zeros: $1,000.00
- Repeating digits: $1,111.11
- Very round: $10,000.00
```

**Example Detection**:
```
🚩 SUSPICIOUS AMOUNT: Unknown Vendor

Transaction: $5,000.00 on Feb 7, 2026
Vendor: "Professional Services LLC"
Amount: Suspiciously round ($5,000.00 exactly)

Red Flags:
• Perfectly round amount
• Vague vendor name
• No prior transactions with this vendor
• Not matching any expected invoice

Action Required: URGENT - Verify authorization
If unauthorized, contact Mercury fraud department immediately
```

### 3. Categorize Anomalies by Severity

**🔴 CRITICAL** (requires immediate action):
- Potential unauthorized charges
- Statistical outliers >5σ
- Suspected fraud patterns
- Duplicate charges >$1,000
- New vendors >$5,000

**🟡 WARNING** (review within 24 hours):
- Statistical outliers 3-5σ
- Price increases >20%
- Frequency anomalies
- Duplicate charges $100-$1,000
- New vendors $1,000-$5,000

**ℹ️ INFORMATIONAL** (review when convenient):
- Minor outliers 2-3σ
- Price increases <20%
- Small duplicates <$100
- New vendors <$1,000

### 4. Provide Context and Recommendations

For each anomaly, provide:

1. **Transaction Details**: Amount, date, vendor, category
2. **Historical Context**: Normal pattern vs current
3. **Severity Assessment**: Critical/Warning/Info
4. **Possible Causes**: Likely explanations
5. **Recommended Actions**: Specific next steps
6. **Resolution Tracking**: Mark as reviewed/resolved

## Output Format

```
═══════════════════════════════════════════════════════════
ANOMALY REPORT
Period: [Date Range]
Anomalies Detected: XX
Critical: X | Warnings: X | Informational: X
═══════════════════════════════════════════════════════════

🚨 CRITICAL ANOMALIES (Immediate Action Required)
─────────────────────────────────────────────────────────
[If any critical anomalies]:

1. [ANOMALY TYPE]: [Vendor]
   Transaction: $X,XXX on [Date]
   Issue: [Description]
   Expected: [Normal pattern]
   Deviation: [How much off]

   Recommended Actions:
   □ [Action 1]
   □ [Action 2]

   [Mark as Reviewed] [Mark as Resolved]

⚠️  WARNING ANOMALIES (Review Within 24 Hours)
─────────────────────────────────────────────────────────
[Similar format for warnings]

ℹ️  INFORMATIONAL (Review When Convenient)
─────────────────────────────────────────────────────────
[Similar format for informational items]

✅ ANOMALY TRENDS
─────────────────────────────────────────────────────────
Last 7 days: X anomalies detected
Last 30 days: XX anomalies detected
Resolution rate: XX% (X resolved, X open)

Most Common Anomaly Types:
1. Statistical outliers: XX%
2. Duplicate charges: XX%
3. Price increases: XX%

📊 SPENDING PATTERN ANALYSIS
─────────────────────────────────────────────────────────
Normal Spending Pattern: Stable ✅ / Variable ⚠️ / Erratic 🔴
Largest Category by Volume: [Category]
Most Variable Category: [Category] (σ = $X,XXX)

Vendors with Most Anomalies:
1. [Vendor]: X anomalies in 90 days
2. [Vendor]: X anomalies
3. [Vendor]: X anomalies

═══════════════════════════════════════════════════════════
```

## Resolution Workflow

### Step 1: Review Flagged Transaction

```
Anomaly: AWS charge $5,200 (expected ~$2,800)

Investigation Checklist:
□ Check AWS billing dashboard for breakdown
□ Review CloudWatch metrics for usage spike
□ Confirm with engineering team (traffic spike? new feature?)
□ Verify invoice matches Mercury transaction
```

### Step 2: Determine Root Cause

**Legitimate Reasons**:
- Business growth (more customers, traffic)
- Planned feature launch (new infrastructure)
- One-time project (data migration, testing)
- Vendor price increase (notification missed)

**Issues Requiring Action**:
- Configuration error (forgot to turn off dev environment)
- Billing error from vendor (dispute charge)
- Unauthorized charge (fraud - contact Mercury)
- Duplicate charge (request refund)

### Step 3: Take Appropriate Action

**If Legitimate**:
```
✅ Mark as Resolved: "Traffic spike from TechCrunch feature"
   Update baseline: New normal is ~$4,500/month
   Adjust budget: Increase infrastructure budget
```

**If Error**:
```
🔧 Action Required: Contact AWS support
   Expected resolution: Refund within 5-7 days
   Track: Add to follow-up list
   Update status: In Progress
```

**If Fraud**:
```
🚨 URGENT: Contact Mercury fraud department
   Freeze account if needed
   File dispute
   Review all other recent transactions
```

### Step 4: Update Detection Model

```
After resolution, update anomaly detection:
- If legitimate growth: Adjust baseline upward
- If seasonal: Note pattern for future reference
- If vendor behavior: Update vendor profile
- If false positive: Tune detection threshold
```

## Use Cases

**Daily Monitoring**:
- "Check today's transactions for anomalies"
- Quick scan of latest charges
- Catch issues within 24 hours

**Weekly Review**:
- "Show me this week's anomaly report"
- Review and resolve flagged items
- Update baseline patterns

**Month-End Close**:
- "Give me all anomalies from last month"
- Verify all transactions before financial close
- Ensure accuracy for board reporting

**Fraud Detection**:
- "Any suspicious charges today?"
- Real-time fraud monitoring
- Protect against unauthorized spending

**Budget Investigation**:
- "Why did we go over budget?"
- Identify unexpected charges
- Understand variance drivers

## Alert Configuration

```json
{
  "real_time_alerts": {
    "enabled": true,
    "channels": ["email", "slack"],
    "thresholds": {
      "critical": {
        "single_transaction": 10000,
        "statistical_outlier_sigma": 5,
        "duplicate_amount": 1000
      },
      "warning": {
        "single_transaction": 5000,
        "statistical_outlier_sigma": 3,
        "price_increase_pct": 20
      }
    }
  },
  "daily_summary": {
    "enabled": true,
    "time": "09:00",
    "include_informational": false
  }
}
```

**Example Real-Time Alert**:
```
📧 Subject: 🚨 Critical Spending Anomaly Detected

Transaction: $8,450 from AWS
Time: Feb 7, 2026 3:42 PM
Expected: ~$2,800
Deviation: +201% (5.2σ)

This charge is significantly higher than your normal AWS spending.

Action Required: Review immediately
View Details: [Link to anomaly report]
```

## Integration with Other Commands

- `/expense-breakdown` - Categorizes expenses, feeds anomaly detection baseline
- `/burn-rate` - Large anomalies can spike burn rate unexpectedly
- `/cost-optimization` - Persistent anomalies may indicate optimization opportunities
- `/budget-variance` - Anomalies often cause budget overruns

## Machine Learning Enhancements

Over time, the anomaly detection improves:

```
Learning from Historical Data:
• Week 1-4: Baseline establishment (many false positives)
• Month 2-3: Pattern recognition improves (fewer false positives)
• Month 3+: Vendor-specific patterns learned (high accuracy)

Adaptive Thresholds:
• AWS: High variability expected (±30% normal)
• Payroll: Very stable (±2% normal)
• Marketing: Moderate variability (±15% normal)

Seasonal Adjustments:
• Q4: Higher marketing spend (holiday season)
• Jan: Lower spend (post-holiday)
• Q2: Higher infrastructure (preparing for growth)
```

## False Positive Management

Not all anomalies are problems:

```
Common False Positives:

1. Legitimate Growth
   - AWS spike due to customer growth (good problem!)
   - More Stripe fees due to more revenue
   - Solution: Update baseline after verification

2. Planned Changes
   - New hire causing payroll increase (expected)
   - Conference attendance (one-time, but planned)
   - Solution: Mark as expected, exclude from future alerts

3. Seasonal Patterns
   - Q4 marketing push
   - Year-end bonuses
   - Solution: Build seasonal models

4. Billing Cycles
   - Annual renewal of monthly subscription
   - Quarterly billing vs monthly
   - Solution: Track billing frequency by vendor
```

## Notes

**Goal: Catch Issues Early**:
- Most billing errors are easier to fix within 30 days
- Fraudulent charges must be reported within 60 days
- Early detection prevents larger problems

**Balance Sensitivity**:
- Too sensitive: Alert fatigue, false positives
- Too lenient: Miss real issues
- Tune over time based on your patterns

**Human Review Required**:
- Algorithms flag anomalies, but humans decide if they're problems
- Context matters: A "spike" might be expected growth
- Always investigate before taking action

**Privacy and Security**:
- Anomaly detection accesses all transaction data
- Reports may contain sensitive vendor/amount info
- Secure access controls recommended
