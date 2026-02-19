---
description: Calculate cash runway and months until you need to raise or reach profitability
argument-hint: ""
---

# Cash Runway Calculator

Calculate how many months of operating cash you have remaining at your current burn rate.

## Usage

```
/runway
```

No arguments needed - uses current Mercury balance and recent burn rate.

## Workflow

### 1. Get Current Cash Balance

Use Mercury MCP to fetch current account balance:
- Primary operating account balance
- Any additional Mercury accounts
- Exclude restricted cash (if any)

If Mercury MCP is not connected:
> Connect Mercury MCP server for automatic balance retrieval. Otherwise, provide your current cash balance manually.

### 2. Calculate Monthly Burn Rate

Either:
- Use cached result from recent `/burn-rate` calculation, OR
- Calculate burn rate from last 3 months of Mercury transactions

See `/burn-rate` command for calculation methodology.

### 3. Calculate Basic Runway

```
Cash Runway (months) = Current Cash Balance / Monthly Burn Rate

Example:
Current Cash: $450,000
Monthly Burn: $75,000/month
Runway: 6.0 months
```

### 4. Adjust for Expected Changes

**Factor in known changes to burn or cash**:

- **Upcoming hires**: If hiring 2 engineers @ $150K each, burn increases by $25K/month
- **Contract expirations**: If major contract ends, burn may decrease
- **Seasonal patterns**: If Q4 marketing spend is higher, adjust accordingly
- **Planned investments**: One-time expenditures coming up

**Factor in expected revenue**:

- If generating revenue, include monthly recurring revenue
- Adjust for expected churn or expansion
- Factor in sales pipeline conversion timing

**Adjusted runway calculation**:
```
Adjusted Monthly Burn = Current Burn + Planned Increases - Expected Revenue
Adjusted Runway = Current Cash / Adjusted Monthly Burn
```

### 5. Scenario Analysis

Present multiple scenarios:

```
RUNWAY SCENARIOS
==================

OPTIMISTIC (Low Burn + High Revenue)
- Assumptions: No new hires, MRR grows 15%/month, reduce AWS spend
- Monthly Burn: $65,000
- Runway: 6.9 months

BASE CASE (Current Trajectory)
- Assumptions: Current burn rate, MRR grows 5%/month
- Monthly Burn: $75,000
- Runway: 6.0 months

CONSERVATIVE (High Burn + Low Revenue)
- Assumptions: Hire 2 engineers, MRR flat, unexpected costs
- Monthly Burn: $100,000
- Runway: 4.5 months
```

### 6. Milestones and Deadlines

Map runway to key dates:

```
RUNWAY TIMELINE
==================

Today: Feb 2026
- Cash Balance: $450,000
- Monthly Burn: $75,000

Aug 2026 (6 months): Runway expires (base case)
- Need to raise or reach profitability

Critical Milestones:
- May 2026 (3 months): Begin fundraising (6mo process = 9mo runway needed)
- Jun 2026 (4 months): Runway < 6 months - reduce burn or bridge round
- Jul 2026 (5 months): Runway < 3 months - critical
```

### 7. Fundraising Timing Guidance

**Runway-Based Fundraise Timing**:

| Current Runway | Action | Urgency |
|----------------|--------|---------|
| 18+ months | Optional - only if opportunity arises | Low |
| 12-18 months | Good time to start exploring | Medium |
| 9-12 months | Begin fundraising NOW (6mo process) | High |
| 6-9 months | Urgent - accelerate fundraise or cut burn | Critical |
| <6 months | Emergency - bridge round or dramatic cuts | Emergency |

**Recommendation**:
Start fundraising when you have **12-15 months runway** to give yourself 6 months for the process while maintaining 6-9 months buffer.

### 8. Burn Reduction Scenarios

If runway is tight, model burn reduction options:

```
EXTEND RUNWAY OPTIONS
==================

Option 1: Freeze Hiring
- Savings: $25,000/month
- Extended Runway: 7.5 months (+1.5 months)
- Impact: Slower product development

Option 2: Reduce Marketing Spend
- Savings: $15,000/month
- Extended Runway: 6.9 months (+0.9 months)
- Impact: Slower customer acquisition

Option 3: Renegotiate Infrastructure
- Savings: $8,000/month
- Extended Runway: 6.5 months (+0.5 months)
- Impact: Minimal

Combined: All three options
- Total Savings: $48,000/month
- New Burn Rate: $27,000/month
- Extended Runway: 16.7 months (+10.7 months!)
```

### 9. Path to Profitability

If revenue is growing, calculate when revenue will exceed burn:

```
PATH TO PROFITABILITY
==================

Current State:
- Monthly Revenue (MRR): $25,000
- Monthly Burn: $75,000
- Gap to Close: $50,000

Revenue Growth Rate: 15% monthly
Months to Profitability: ~8 months (Oct 2026)

Projected:
- Oct 2026 MRR: $76,000
- Oct 2026 Burn: $75,000 (assumed flat)
- Cash Remaining: ~$150,000

Conclusion: Runway sufficient to reach profitability IF:
✓ Revenue maintains 15% growth
✓ Burn stays flat (no major hiring)
✓ No unexpected expenses
```

## Output Format

```
CASH RUNWAY ANALYSIS
As of: [Today's Date]
Data Source: Mercury Bank

CURRENT POSITION
==================
Cash Balance: $XXX,XXX
Monthly Burn Rate: $XX,XXX/month
Runway: X.X months
Zero Cash Date: [Month Year]

SCENARIO ANALYSIS
==================
[Optimistic/Base/Conservative scenarios]

FUNDRAISING GUIDANCE
==================
Status: [Color-coded urgency]
Recommendation: [Specific action]
Timeline: [When to start]

PATH TO PROFITABILITY
==================
[If applicable]

BURN REDUCTION OPTIONS
==================
[If runway <9 months]
```

## Alerts

**🚨 CRITICAL (<6 months runway)**:
- Immediate action required
- Begin emergency fundraise or implement burn cuts NOW
- Prepare for bridge round or down round scenarios

**⚠️ WARNING (6-9 months runway)**:
- Start fundraising process immediately
- Begin modeling burn reduction scenarios
- Update financial projections for investors

**ℹ️ HEALTHY (>12 months runway)**:
- Continue monitoring monthly
- Plan for fundraise when runway hits 12 months
- Focus on growth and efficiency

## Next Steps

Suggest based on runway status:

- If runway <9 months: Run `/cost-optimization` to find burn reduction opportunities
- If fundraising: Run `/investor-packet` to prepare materials
- Always: Run `/financial-snapshot` for complete picture

## Continuous Monitoring with Agents

For proactive runway tracking, use the **runway-monitor agent**:

**When to use:**
- After running this command, invoke the agent for daily monitoring
- Set up automatic daily checks (9 AM recommended)
- Critical when runway <12 months (fundraising zone)

**How to invoke:**
```
Use the runway-monitor agent to track my cash runway daily
```

**What it does:**
- Monitors Mercury balance changes daily
- Alerts when crossing critical thresholds (12mo, 9mo, 6mo, 3mo)
- Tracks fundraising timeline automatically
- Flags unexpected burn increases
- Updates scenario projections continuously

**Benefits:**
- Never miss a critical runway milestone
- Proactive alerts before problems become urgent
- Automated fundraising timeline tracking
- Peace of mind with 24/7 monitoring
