---
description: Identify specific cost savings opportunities across all expense categories
argument-hint: ""
---

# Cost Optimization

Analyze all expenses and identify specific, actionable opportunities to reduce costs without impacting growth or operations.

## Usage

```
/cost-optimization
```

No arguments needed - analyzes all recent spending to find savings.

## Workflow

### 1. Analyze Expense Patterns

Pull last 90 days of Mercury transactions and analyze:
- Recurring subscriptions and their usage
- Vendor pricing and contract terms
- Duplicate or redundant services
- Over-provisioned resources
- Optimization opportunities by category

### 2. SaaS Subscription Audit

Identify underutilized or redundant SaaS:

```
SaaS OPTIMIZATION OPPORTUNITIES
────────────────────────────────────────

1. Zoom Business (Video Conferencing)
   Current: $150/month (5 host licenses)
   Usage: 2 active hosts, avg 3 meetings/week
   Recommendation: Downgrade to Pro (3 hosts)
   Savings: $30/month ($360/year)
   Impact: Low (3 hosts sufficient for current usage)

2. Notion Team Plan (Collaboration)
   Current: $200/month (10 seats)
   Usage: 3 active users in last 30 days
   Recommendation: Downgrade to Plus (5 seats) or free plan
   Savings: $120/month ($1,440/year)
   Impact: Low (most features unused, 3 users sufficient)

3. Slack Business+ (Communication)
   Current: $680/month (8 users)
   Usage: Advanced features not used (compliance, SSO, etc.)
   Recommendation: Downgrade to Business
   Savings: $230/month ($2,760/year)
   Impact: None (not using premium features)

4. CircleCI Team Plan (CI/CD)
   Current: $150/month
   Alternative: GitHub Actions (included in current plan)
   Recommendation: Migrate to GitHub Actions
   Savings: $150/month ($1,800/year)
   Impact: Low (2-3 days migration work)

Total SaaS Savings: $530/month ($6,360/year)
Implementation Effort: 1-2 weeks
```

### 3. Infrastructure Right-Sizing

Analyze cloud spending for optimization:

```
INFRASTRUCTURE OPTIMIZATION
────────────────────────────────────────

AWS OPTIMIZATIONS:

1. EC2 Reserved Instances
   Current: On-demand pricing ($1,680/month)
   Recommendation: 1-year reserved instances
   Savings: $504/month ($6,048/year) - 30% discount
   Requirements:
   - Identify stable baseline usage: 2 large instances always running
   - 1-year commitment
   Impact: None (resources already running 24/7)

2. Right-Size Over-Provisioned Instances
   Current: 2x m5.2xlarge instances (8 vCPU, 32GB RAM each)
   Usage: Avg 25% CPU, 40% memory
   Recommendation: Downgrade to m5.xlarge (4 vCPU, 16GB RAM)
   Savings: $220/month ($2,640/year)
   Impact: Low (still 2x headroom on current usage)
   Risk: Monitor for 1 week after change

3. S3 Storage Optimization
   Current: 800GB in S3 Standard ($18/month)
   Analysis: 60% of data not accessed in 90+ days
   Recommendation: Implement S3 Lifecycle policies
   - Move to S3 Infrequent Access after 90 days (save 45%)
   - Move to Glacier after 1 year (save 80%)
   Savings: $60/month ($720/year) when fully implemented
   Impact: None (access patterns unchanged)

4. Auto-Scaling Configuration
   Current: 4 instances running 24/7
   Usage: Peak traffic 9AM-6PM weekdays (8x off-peak)
   Recommendation: Configure auto-scaling
   - Min: 1 instance (off-peak)
   - Max: 4 instances (peak)
   - Scale based on CPU >70%
   Savings: $450/month ($5,400/year) - 40% reduction
   Impact: None (performance maintained during peak)

5. RDS Database Optimization
   Current: RDS db.m5.large ($560/month)
   Usage: Avg 30% CPU, 50% IOPS
   Options:
   - Reserved instance: Save $168/month (30% discount)
   - Downsize to db.m5.medium: Save $280/month
   Recommendation: Reserved + downsize to medium
   Savings: $348/month ($4,176/year)
   Impact: Monitor closely, may need to upsize later

Total Infrastructure Savings: $1,582/month ($18,984/year)
Implementation Effort: 2-3 weeks
```

### 4. Vendor Consolidation

Identify redundant tools that can be consolidated:

```
VENDOR CONSOLIDATION OPPORTUNITIES
────────────────────────────────────────

1. Monitoring & Observability
   Current State:
   - Datadog APM: $1,500/month
   - Sentry Error Tracking: $800/month
   - PagerDuty Alerting: $300/month
   Total: $2,600/month

   Consolidated Option A: Datadog only (add error tracking)
   - Datadog Full Suite: $2,200/month
   - Savings: $400/month ($4,800/year)
   - Impact: Unified platform, better correlation

   Consolidated Option B: Open source stack
   - Self-hosted Prometheus + Grafana + AlertManager: $0
   - Infrastructure cost: ~$200/month
   - Savings: $2,400/month ($28,800/year)
   - Impact: High (need DevOps time to setup/maintain)
   - Recommended: Not for current team size

   Recommendation: Option A (Datadog consolidation)

2. Communication Tools
   Current State:
   - Zoom: $150/month
   - Google Meet (included in Workspace): $0
   - Loom: $80/month
   Total: $230/month

   Consolidation:
   - Use Google Meet for all video calls: Free
   - Keep Loom for async video: $80/month
   Savings: $150/month ($1,800/year)
   Impact: Low (Google Meet comparable quality)

Total Consolidation Savings: $550/month ($6,600/year)
```

### 5. Contract Renegotiation

Identify upcoming renewals for negotiation:

```
CONTRACT RENEGOTIATION OPPORTUNITIES
────────────────────────────────────────

1. AWS (Renewal: April 2026)
   Current: $2,800/month on-demand
   Strategy:
   - Commit to reserved instances ($500/month savings)
   - Negotiate Enterprise Discount Program (5-10% off)
   - Request credits for new features adoption
   Expected Savings: $600/month ($7,200/year)
   Action: Begin talks 60 days before renewal

2. HubSpot Marketing (Renewal: March 2026)
   Current: $800/month (Professional plan)
   Strategy:
   - Review actual usage (may be over-provisioned)
   - Request multi-year discount (15-20%)
   - Negotiate based on usage (contacts, emails)
   Expected Savings: $120/month ($1,440/year)
   Action: Contact rep now (renewal in 30 days)

3. GitHub Enterprise (Renewal: June 2026)
   Current: $1,200/month (50 seats)
   Usage: 32 active developers
   Strategy:
   - Reduce to 35 seats
   - Annual prepayment (10% discount)
   Expected Savings: $180/month ($2,160/year)
   Action: Begin talks 90 days out

Total Renegotiation Savings: $900/month ($10,800/year)
```

### 6. Payment Optimization

Optimize payment timing and methods:

```
PAYMENT OPTIMIZATION
────────────────────────────────────────

1. Annual Prepayment Discounts
   Current Monthly SaaS: $8,200/month
   Annual prepay eligible: $6,500/month worth

   If paid annually:
   - Typical discount: 15-20%
   - Savings: $975-1,300/month ($11,700-15,600/year)
   - Upfront cost: $66,300 (vs $78,000 paid monthly)

   Cash flow consideration:
   - Current cash: $585K
   - Runway impact: -2 weeks (one-time)
   - ROI: 18-24% annually

   Recommendation:
   - Prepay top 5 vendors annually
   - Estimated savings: $800/month

2. Credit Card Rewards
   Current: Business debit card (no rewards)
   Opportunity: Business credit card with 2% cash back
   Monthly spend eligible: ~$30,000
   Rewards: $600/month ($7,200/year)

   Recommendation: Apply for business credit card
   - Brex, Ramp, or Amex Business Platinum
   - 2% cash back or equivalent points
   - Pay off monthly (no interest)

Total Payment Optimization: $1,400/month ($16,800/year)
```

### 7. Process Automation

Identify manual processes that can be automated to reduce contractor/labor costs:

```
AUTOMATION OPPORTUNITIES
────────────────────────────────────

1. Customer Support (Contractor: $3,500/month)
   Current: 40 hours/week contractor for tier-1 support
   Opportunity: Implement Intercom + chatbot
   - Chatbot handles 60% of tier-1 (FAQs, docs, basic troubleshooting)
   - Reduces contractor to 15 hours/week
   Cost: $200/month (Intercom) + $200 (chatbot setup)
   Savings: $2,200/month ($26,400/year)
   Implementation: 2 weeks

2. Invoice Processing (Finance contractor: $1,200/month)
   Current: 10 hours/month for invoice entry and reconciliation
   Opportunity: Bill.com or Ramp automated AP
   - OCR invoice scanning
   - Auto-categorization and approval workflows
   Cost: $150/month
   Savings: $800/month ($9,600/year)
   Implementation: 1 week

3. Expense Reporting (Employee time: 8 hours/month)
   Current: Manual expense submissions and approvals
   Opportunity: Ramp or Brex with auto-categorization
   - Eliminates monthly expense reports
   - Real-time visibility
   Cost: $0 (included in card platform)
   Savings: $400/month equivalent time ($4,800/year)
   Implementation: 2 weeks

Total Automation Savings: $3,400/month ($40,800/year)
```

### 8. Strategic Spend Cuts

If aggressive savings needed (runway <6 months):

```
STRATEGIC COST REDUCTION (If Needed)
────────────────────────────────────────

TIER 1: Low Impact, High Savings
• Freeze hiring (2 planned engineers): -$25,000/month
• Pause paid marketing (Google/LinkedIn): -$7,000/month
• Annual prepay top SaaS (timing savings): -$800/month
Total: -$32,800/month

TIER 2: Medium Impact, Medium Savings
• Reduce contractor hours 50%: -$2,500/month
• Downgrade/cancel non-essential SaaS: -$1,200/month
• Office to co-working space: -$2,000/month
Total: -$5,700/month

TIER 3: High Impact, Very High Savings (Last Resort)
• Reduce headcount 20% (2 people): -$16,000/month
• Cut all marketing spend: -$9,200/month
• Move to cheaper infrastructure: -$1,500/month
Total: -$26,700/month

TOTAL POTENTIAL BURN REDUCTION: -$65,200/month
Impact on runway: 5.5 months → 13.2 months
```

## Output Format

```
═══════════════════════════════════════════════════════════
COST OPTIMIZATION OPPORTUNITIES
Analysis Date: [Date]
Total Potential Savings: $X,XXX/month ($XX,XXX/year)
═══════════════════════════════════════════════════════════

💰 EXECUTIVE SUMMARY
─────────────────────────────────────────────────────────
Priority Opportunities:
• SaaS Optimization: $XXX/month
• Infrastructure: $X,XXX/month
• Vendor Consolidation: $XXX/month
• Contract Renegotiation: $XXX/month
• Payment Optimization: $XXX/month
• Process Automation: $X,XXX/month
───────────────────────────────────────────────────────
TOTAL: $X,XXX/month ($XX,XXX/year)

Implementation Effort: X-X weeks
Impact on Operations: Low to Medium

🔝 TOP 5 QUICK WINS
─────────────────────────────────────────────────────────
1. [Opportunity]: -$XXX/month (1 day to implement)
2. [Opportunity]: -$XXX/month (3 days)
3. [Opportunity]: -$XXX/month (1 week)
4. [Opportunity]: -$XXX/month (1 week)
5. [Opportunity]: -$XXX/month (2 weeks)

🏢 DETAILED OPPORTUNITIES BY CATEGORY
─────────────────────────────────────────────────────────
[Detailed breakdown by category with specific actions]

📊 SAVINGS TIMELINE
─────────────────────────────────────────────────────────
Immediate (This Week): $XXX/month
Short-term (This Month): $XXX/month
Medium-term (This Quarter): $XXX/month

📈 IMPACT ANALYSIS
─────────────────────────────────────────────────────────
Current Burn: $XX,XXX/month
After Optimization: $XX,XXX/month (-XX%)
Runway Extension: +X.X months

═══════════════════════════════════════════════════════════
```

## Implementation Roadmap

```
WEEK 1: Quick Wins (Save $1,200/month)
□ Downgrade Zoom to Pro
□ Cancel CircleCI, migrate to GitHub Actions
□ Reduce Notion seats
□ Apply for business credit card

WEEK 2-3: SaaS & Infrastructure (Save $2,100/month)
□ AWS reserved instances (order now, save next month)
□ Right-size EC2 instances
□ Implement S3 lifecycle policies
□ Downgrade Slack plan
□ Consolidate monitoring (Datadog)

WEEK 4-6: Contracts & Automation (Save $4,300/month)
□ Renegotiate HubSpot (renewal soon)
□ Implement Intercom + chatbot
□ Setup Bill.com or Ramp AP automation
□ Annual prepay top 5 SaaS vendors

ONGOING: Continuous Optimization
□ Monthly SaaS audit (check for unused tools)
□ Quarterly contract reviews
□ Monitor AWS cost anomalies weekly
□ Review automation opportunities monthly

Total Savings After 6 Weeks: $7,600/month
Runway Extension: +2.1 months
```

## Use Cases

**Proactive Optimization**:
- "What can I do to reduce costs?"
- Regular quarterly cost reviews
- Maintain healthy burn efficiency

**Runway Extension**:
- "I need to extend runway by 3 months"
- Identify specific savings to hit target
- Prioritize low-impact cuts

**Budget Management**:
- "How can I stay within budget?"
- Find savings in over-budget categories
- Reallocate savings to growth areas

**Board Preparation**:
- "Show me we're being capital efficient"
- Demonstrate ongoing optimization efforts
- Highlight efficiency improvements

## Alerts

**High-Priority Opportunities** (>$500/month savings):
- Flag immediately for founder review
- Typically low effort, high impact
- Should be implemented quickly

**Contract Renewals** (60-90 days out):
- Proactive negotiation opportunity
- Research competitive pricing
- Prepare usage analysis for negotiation

**Unused Services** (no usage in 30 days):
- Automatically flag for cancellation
- Verify with team before canceling
- Track savings from cancellations

## Related Commands

- `/expense-breakdown` - See detailed expense categories to identify optimization targets
- `/budget-variance` - Compare optimized spend vs budget
- `/burn-rate` - See impact of optimizations on overall burn (startup-finance plugin)
- `/runway` - See how optimizations extend cash runway (startup-finance plugin)

## Continuous Optimization with Agents

For ongoing cost optimization, use these agents:

### burn-analyzer Agent (from startup-finance plugin)

**When to use:**
- After running this command for implementation
- Weekly for continuous optimization monitoring
- Before quarterly budget planning

**How to invoke:**
```
Use the burn-analyzer agent to continuously monitor spending and identify new optimization opportunities
```

**What it does:**
- Analyzes all transactions weekly
- Identifies new cost optimization opportunities automatically
- Tracks savings from implemented optimizations
- Flags new SaaS subscriptions that may be redundant
- Monitors for price increases to renegotiate

### anomaly-detector-agent Agent

**When to use:**
- For real-time fraud and error detection
- To catch duplicate charges immediately
- To monitor unexpected spending spikes

**How to invoke:**
```
Use the anomaly-detector-agent to monitor transactions 24/7 for anomalies and potential savings
```

**What it does:**
- 24/7 transaction monitoring
- Detects duplicate charges for refunds
- Flags suspicious transactions
- Identifies price increases immediately
- Alerts on billing errors

**Combined Benefits:**
- Continuous cost optimization (not one-time)
- Catch billing errors within hours (not months)
- Automatic identification of new savings opportunities
- Track optimization impact over time

## Notes

**Balance Optimization with Growth**:
- Don't cut expenses that drive revenue
- Marketing with positive ROI should not be cut
- Infrastructure supporting growth is good spend
- Focus on waste, redundancy, and inefficiency

**Implementation Velocity**:
- Quick wins first (low-hanging fruit)
- Prioritize by savings / effort ratio
- Don't boil the ocean - pick top 10 opportunities

**Ongoing Optimization**:
- Cost optimization is continuous, not one-time
- Review quarterly at minimum
- Build a culture of efficiency, not frugality

**When NOT to Optimize**:
- When fundraising is imminent (focus on growth story)
- When runway is healthy (>12 months)
- When optimizations hurt team productivity
- When savings are <$100/month (not worth the effort)
