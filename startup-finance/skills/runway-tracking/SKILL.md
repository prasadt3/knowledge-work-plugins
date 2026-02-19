---
title: Cash Runway Tracking & Fundraising Timing
description: Comprehensive methodology for calculating cash runway, scenario planning, and determining optimal fundraising timing
category: finance
tags: [runway, fundraising, cash-management, startup-finance]
---

# Cash Runway Tracking & Fundraising Timing

## Overview

Cash runway is the number of months a startup can operate before running out of money. It's the single most important metric for startup survival.

This skill provides comprehensive knowledge of runway calculation, scenario planning, and fundraising timing for startup founders.

## Core Concepts

### What is Cash Runway?

**Cash Runway** = Cash Balance / Monthly Burn Rate

**Example**:
```
Current Cash: $450,000
Monthly Burn: $75,000/month
Runway: 6.0 months
Zero Cash Date: ~August 2026 (if today is February 2026)
```

### Why Runway Matters

1. **Survival Clock** - Shows exactly when you'll run out of money
2. **Fundraising Trigger** - Determines when to start raising (need 12-15 months to begin)
3. **Strategic Decisions** - Guides hiring, spending, and growth investments
4. **Investor Signal** - VCs want to see 12-18+ months runway after they invest

### Types of Runway

**1. Cash Runway** (most common):
```
Runway = Cash in Bank / Monthly Burn Rate
```
Assumes burn stays constant, no additional revenue.

**2. Adjusted Runway** (more realistic):
```
Adjusted Runway = Cash / (Burn - Monthly Revenue Growth)
```
Factors in growing revenue reducing effective burn.

**3. Scenario-Based Runway** (best for planning):
- Optimistic: Best case (low burn, high revenue growth)
- Base case: Current trajectory (most likely)
- Conservative: Worst case (high burn, low revenue growth)

## Runway Calculation Methodology

### Step 1: Determine Current Cash Balance

**What to Include**:
- ✅ Operating account balance
- ✅ Liquid savings accounts
- ✅ Money market accounts

**What to Exclude**:
- ❌ Restricted cash (legal escrow, customer deposits)
- ❌ Accounts receivable (not yet received)
- ❌ Investments that can't be liquidated quickly
- ❌ Equipment or other assets (not cash)

**Example**:
```
Mercury Operating Account: $385,000
Mercury Savings Account: $200,000
Restricted (customer deposits): $50,000 ❌
──────────────────────────────────
Available Cash: $585,000
```

### Step 2: Calculate Monthly Burn Rate

Use **90-day rolling average** for accuracy (see burn-analysis skill).

**Example**:
```
Last 3 months total expenses: $225,000
Monthly average: $75,000/month
```

### Step 3: Calculate Base Runway

```
Runway = Available Cash / Monthly Burn

Example:
$585,000 / $75,000 = 7.8 months
```

If today is February 7, 2026:
- Runway expires: ~October 1, 2026
- This is your "zero cash date"

### Step 4: Adjust for Known Changes

**Factor in planned changes** to burn or cash:

**Burn Increases**:
```
Current Burn: $75,000/month
+ 2 engineers starting March: +$25,000/month (new burn: $100K)
+ AWS reserved instance: +$5,000/month upfront
──────────────────────────────────
New Burn (starting March): $100,000/month
```

**Revenue Increases**:
```
Current MRR: $25,000
Growing at 10%/month
In 3 months: ~$33,000
Reduces effective burn by $8,000
```

**Adjusted Calculation**:
```
Today (Feb): $585K / $75K = 7.8 months
Starting March: $585K / ($100K - revenue growth effect)

Month-by-month:
Feb: -$75K → $510K remaining (6.8mo runway)
Mar: -$100K → $410K remaining (4.1mo runway)
Apr: -$100K → $310K remaining (3.1mo runway)
...

Adjusted runway: ~5.5 months (accounts for burn increase)
```

### Step 5: Scenario Analysis

Create three scenarios to bound your planning:

**OPTIMISTIC Scenario** (best case):
- Assumptions: No new hires, revenue grows 15%/mo, cut AWS costs by $10K
- Burn: $65,000/month → decreasing over time due to revenue
- Runway: 9+ months

**BASE CASE Scenario** (most likely):
- Assumptions: Hire 2 engineers, revenue grows 10%/mo, current infrastructure
- Burn: $100,000/month → decreasing slowly due to revenue
- Runway: 5.5 months

**CONSERVATIVE Scenario** (worst case):
- Assumptions: Hire 2 engineers + 1 sales, revenue growth slows to 5%/mo, AWS spike
- Burn: $115,000/month → flat or increasing
- Runway: 4.5 months

## Fundraising Timing Framework

### The 12-15 Month Rule

**Start fundraising when you have 12-15 months of runway.**

Why?
- Fundraising typically takes 4-6 months
- You want 6-9 months buffer after raising
- Rushing with <6 months runway weakens negotiating position
- Investors worry about "distressed" companies with short runway

### Fundraising Timeline

**Typical Seed/Series A fundraise timeline**:

```
Month 0 (15 months runway):
├─ Preparation phase begins
├─ Update financial model
├─ Prepare pitch deck
└─ Identify target investors

Month 1-2 (13-14 months runway):
├─ Warm introductions to investors
├─ Initial meetings (exploratory)
├─ Refine messaging based on feedback
└─ Build pipeline of 30-50 potential investors

Month 3-4 (11-12 months runway):
├─ Active fundraising (20-30 meetings/month)
├─ Partner meetings at interested firms
├─ First term sheets (if going well)
└─ Negotiate terms

Month 5-6 (9-10 months runway):
├─ Due diligence
├─ Finalize term sheet
├─ Legal documentation
└─ Close round

Result: Runway extended to 18-24 months
```

**If you wait until 6 months runway** to start:
- Month 6: Rushed preparation, weak positioning
- Months 6-9: Frantic fundraising, taking any term sheet
- Months 9-10: Due diligence (burning final cash)
- Month 10-11: Close or die trying
- Result: Desperation fundraise, bad terms, or failure

### Runway-Based Action Guide

| Runway Remaining | Status | Action Required | Urgency |
|------------------|--------|-----------------|---------|
| **18+ months** | 🟢 Healthy | Optional fundraising (only if great opportunity) | Low |
| **12-18 months** | 🟢 Good | Begin fundraising preparation | Medium |
| **9-12 months** | 🟡 Caution | **Start fundraising NOW** | High |
| **6-9 months** | 🟠 Warning | Accelerate fundraise or cut burn significantly | Critical |
| **3-6 months** | 🔴 Danger | Emergency measures: bridge round or dramatic cuts | Emergency |
| **<3 months** | 🔴🔴 Crisis | Survival mode: layoffs, bridge, or shut down | Existential |

### Bridge Rounds

**When to consider a bridge round**:
- Runway <6 months and full raise will take too long
- Need 3-6 months extension to hit key milestone
- Have committed lead for Series A but need time for diligence

**Bridge round structure**:
- $200K-$1M (smaller than full round)
- Fast close (2-4 weeks)
- Often convertible notes or SAFEs
- From existing investors or angels

**Example**:
```
Current situation:
- Runway: 4 months
- Burn: $100K/month
- Need: $400K to extend 4 months → 8 months total

Bridge round:
- Raise $500K on SAFE (note or note)
- Close in 3 weeks
- New runway: 9 months
- Use time to properly fundraise Series A
```

## Runway Extension Strategies

### 1. Reduce Burn (Fast Impact)

**Immediate cuts** (implement this week):
- Hiring freeze (save $25K-50K/month per position)
- Pause paid marketing (save $10K-30K/month)
- Cancel unused SaaS (save $5K-15K/month)
- Reduce cloud costs (reserved instances, right-sizing: save $5K-20K/month)

**Example**:
```
Current Burn: $100K/month
Runway: 5.5 months

Actions:
- Freeze 2 planned hires: -$25K/month
- Pause Google Ads: -$15K/month
- SaaS audit: -$5K/month
──────────────────────────────────
New Burn: $55K/month
New Runway: $585K / $55K = 10.6 months

Extension: +5.1 months!
```

### 2. Grow Revenue (Medium Impact)

**Accelerate revenue** to reduce net burn:
- Price increases (10-20% can be implemented quickly)
- Upsells to existing customers (faster than new acquisition)
- Faster sales cycles (focus on smaller deals that close quicker)
- Annual prepayments (get 12 months cash upfront)

**Example**:
```
Current MRR: $25K, Burn: $100K → Net burn: $75K
Runway: 7.8 months

Actions:
- 20% price increase on renewals: +$5K MRR
- Upsell 5 customers to annual: +$60K cash upfront, +$10K MRR
- Close 3 deals faster: +$5K MRR
──────────────────────────────────
New MRR: $45K, Net Burn: $55K
New Runway: ($585K + $60K upfront) / $55K = 11.7 months

Extension: +3.9 months
```

### 3. Increase Cash (Immediate Impact)

**Add cash without raising**:
- Venture debt (10-30% of last round, 1-2 months to close)
- Revenue-based financing (if SaaS with MRR)
- R&D tax credits (if you qualify)
- Customer prepayments (annual plans)
- Asset sales (equipment, IP)

**Example (Venture Debt)**:
```
Last round: $2M Series A
Debt available: $500K (25% of round)
Terms: 12% interest, 3-year term, 12-month interest-only

Impact:
Cash: +$500K immediately
Burn: +$5K/month (interest only)
Runway: ($585K + $500K) / $105K = 10.3 months

Extension: +2.5 months (with minimal dilution)
```

## Path to Profitability

### When Runway Exceeds Profitability Timeline

**Best case scenario**: Your revenue is growing fast enough to reach profitability before running out of cash.

**Calculation**:
```
Current State:
- Cash: $585K
- Monthly Burn: $75K
- Monthly Revenue: $25K
- Revenue Growth Rate: 15%/month
- Runway: 7.8 months

Question: Will revenue cover burn before cash runs out?

Month-by-month projection:
Month 1: Revenue: $25K, Burn: $75K, Net: -$50K, Cash: $535K
Month 2: Revenue: $29K, Burn: $75K, Net: -$46K, Cash: $489K
Month 3: Revenue: $33K, Burn: $75K, Net: -$42K, Cash: $447K
Month 4: Revenue: $38K, Burn: $75K, Net: -$37K, Cash: $410K
Month 5: Revenue: $44K, Burn: $75K, Net: -$31K, Cash: $379K
Month 6: Revenue: $51K, Burn: $75K, Net: -$24K, Cash: $355K
Month 7: Revenue: $58K, Burn: $75K, Net: -$17K, Cash: $338K
Month 8: Revenue: $67K, Burn: $75K, Net: -$8K, Cash: $330K
Month 9: Revenue: $77K, Burn: $75K, Net: +$2K, Cash: $332K ✅

PROFITABLE at month 9!
Cash remaining: $332K
Conclusion: No fundraising needed if growth continues!
```

### Breakeven Analysis

**Calculate time to profitability**:

```
Revenue needed to break even = Monthly Burn
Current revenue = MRR
Monthly growth rate = r

Formula: MRR × (1 + r)^n = Burn
Solve for n (months to breakeven)

n = ln(Burn / MRR) / ln(1 + r)
```

**Example**:
```
MRR: $25K
Burn: $75K
Growth rate: 15%/month (0.15)

n = ln(75/25) / ln(1.15)
n = ln(3) / ln(1.15)
n = 1.099 / 0.140
n ≈ 7.8 months to break even

Runway: 7.8 months

Conclusion: You will barely make it! Need to either:
- Accelerate revenue growth to >15%/month, OR
- Reduce burn slightly, OR
- Raise a small bridge to add buffer
```

## Runway Monitoring Best Practices

### Daily Monitoring

**What to check daily** (if runway <6 months):
- Bank account balance
- Large transactions (>$5K)
- Unexpected charges

**Tools**:
- Bank alerts for low balance
- Daily balance email from bank
- Dashboard showing runway countdown

### Weekly Monitoring

**What to track weekly**:
- 7-day rolling burn rate
- Runway calculation (updated with latest burn)
- Upcoming expenses (next 30 days)
- Revenue trajectory

**Weekly runway report**:
```
Week of Feb 7, 2026
─────────────────────
Cash: $585K
7-day burn: $17.5K ($75K/month pace)
Runway: 7.8 months
Status: 🟡 Caution (start fundraising)

Upcoming expenses (next 30 days):
- Feb 15: Payroll $42K
- Feb 28: AWS $2.8K
- Mar 1: Office rent $3.5K
- Mar 15: Payroll $42K
Total: $90.3K

Projected cash March 15: $495K
Projected runway March 15: 6.6 months
```

### Monthly Monitoring

**What to analyze monthly**:
- Month-end runway calculation
- Burn vs budget
- Scenario updates (optimistic/base/conservative)
- Fundraising timeline check

**Monthly board report section**:
```
CASH & RUNWAY (January 2026)
──────────────────────────────────
Cash (1/31): $585K
Monthly Burn: $75K
Runway: 7.8 months
Zero Cash Date: Oct 1, 2026

Burn Detail:
- Payroll: $48K (64%)
- Infrastructure: $12K (16%)
- Marketing: $10K (13%)
- G&A: $5K (7%)

Scenarios:
- Base: 7.8 months
- Conservative: 6.1 months (if hiring proceeds)
- Optimistic: 9.5 months (if revenue accelerates)

Fundraising Status:
- Action: Begin preparation (at 7.8mo runway threshold)
- Timeline: Target close in June (maintain 4mo buffer)
```

## Red Flags and Warning Signs

### Runway Red Flags

🚩 **Runway Decreasing Faster Than Expected**:
- Expected: 1 month per month (linear)
- Actual: 1.5 months per month (burn increasing)
- Cause: Uncontrolled spending or revenue shortfall

🚩 **Unexpected Large Expenses**:
- One-time costs >10% of monthly burn
- Legal fees, settlement, equipment failure
- Impact: Sudden runway drop

🚩 **Revenue Growth Stalling**:
- Path to profitability assumes growth
- If growth slows, profitability timeline extends
- May need to fundraise instead

🚩 **Burn Increasing Without Plan**:
- Burn should only increase with deliberate decisions (hires, campaigns)
- Unexplained burn growth = lack of control

### Crisis Management

**If runway drops below 3 months unexpectedly**:

**Week 1 (Emergency Assessment)**:
- Calculate exact runway (down to the week)
- Identify all upcoming expenses
- Model burn reduction scenarios
- Assess bridge round feasibility

**Week 2-3 (Immediate Actions)**:
- Implement emergency burn cuts
  - Hiring freeze
  - Marketing pause
  - Defer non-critical expenses
- Reach out to existing investors for bridge
- Alert board immediately

**Week 4+ (Stabilize)**:
- Execute bridge round if available
- Or implement layoffs if necessary (20-40% reduction)
- Extend runway to 6+ months minimum
- Resume fundraising from position of stability (not desperation)

## Conclusion

Cash runway is your startup's survival clock. Key principles:

1. **Calculate accurately**: Use available cash and realistic burn rate
2. **Monitor constantly**: Weekly at minimum, daily if <6 months runway
3. **Plan scenarios**: Always know optimistic/base/conservative cases
4. **Fundraise proactively**: Start at 12-15 months, never <9 months
5. **Extend strategically**: Burn reduction, revenue growth, or bridge rounds
6. **Path to profitability**: Best outcome is growing into profitability

**The goal is never to run out of runway.** Maintain 12-18 months at all times through a combination of fundraising, revenue growth, and disciplined spending.

**Remember**: Runway gives you **time**, and time is your most valuable resource as a startup. Time to find product-market fit, time to grow revenue, time to hire great people, and time to fundraise from a position of strength rather than desperation.
