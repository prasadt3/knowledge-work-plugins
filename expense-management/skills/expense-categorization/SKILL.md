---
title: Expense Categorization & Chart of Accounts
description: Best practices for categorizing startup expenses and maintaining clean financial records
category: finance
tags: [expense-categorization, accounting, chart-of-accounts, bookkeeping]
---

# Expense Categorization & Chart of Accounts

## Overview

Proper expense categorization is essential for financial reporting, tax preparation, budget management, and understanding where your startup's money is going.

This skill provides comprehensive knowledge of expense categorization best practices, standard category structures, and how to maintain clean, consistent financial records.

## Why Expense Categorization Matters

1. **Financial Reporting** - Generate accurate P&L statements and expense reports
2. **Budget Management** - Track spending against budgets by category
3. **Tax Preparation** - Identify deductible expenses and support tax filings
4. **Investor Reporting** - Show investors where capital is being deployed
5. **Cost Analysis** - Identify optimization opportunities and spending patterns
6. **Burn Rate Calculation** - Accurately calculate and forecast cash burn

## Standard SaaS Startup Category Structure

### Level 1: Major Categories

Most SaaS startups use these 4-5 major categories:

```
1. COST OF GOODS SOLD (COGS) - 5-20% of revenue
   └─ Direct costs to deliver the product/service

2. RESEARCH & DEVELOPMENT (R&D) / PERSONNEL - 50-70% of spend
   └─ Product development, engineering, design

3. SALES & MARKETING (S&M) - 10-30% of spend
   └─ Customer acquisition and revenue generation

4. GENERAL & ADMINISTRATIVE (G&A) - 5-15% of spend
   └─ Overhead and support functions

5. COST OF REVENUE (if separate from COGS)
   └─ Support, success, hosting infrastructure
```

### Level 2: Subcategories

**COST OF GOODS SOLD**:
```
• Hosting & Infrastructure
  - Cloud providers (AWS, GCP, Azure)
  - CDN (CloudFlare, Fastly)
  - Database hosting
• Third-party Services
  - Payment processing fees (Stripe, PayPal)
  - SMS/email delivery (Twilio, SendGrid)
  - API costs directly tied to product delivery
• Customer Support (if high-touch)
  - Support team salaries/contractors
  - Support tools (Zendesk, Intercom)
```

**RESEARCH & DEVELOPMENT**:
```
• Engineering Salaries & Benefits
  - Software engineers
  - DevOps/SRE
  - Engineering managers
  - Payroll taxes and benefits
• Product & Design
  - Product managers
  - Designers
  - UX researchers
• Contractors
  - Engineering contractors
  - Design contractors
• Development Tools
  - IDEs, GitHub, CI/CD
  - Development infrastructure
  - Testing and QA tools
```

**SALES & MARKETING**:
```
• Advertising
  - Google Ads
  - LinkedIn Ads
  - Meta Ads
  - Display advertising
• Marketing Team
  - Marketing salaries and benefits
  - Marketing contractors and agencies
• Marketing Tools & Software
  - CRM (HubSpot, Salesforce)
  - Email marketing (Mailchimp, Customer.io)
  - Analytics (Mixpanel, Amplitude)
  - SEO tools
• Events & Conferences
  - Booth fees
  - Sponsorships
  - Travel for events
• Content & Brand
  - Content creation
  - Design and creative
  - PR and communications
• Sales Team (if separate)
  - Sales salaries and commissions
  - Sales tools
  - Travel
```

**GENERAL & ADMINISTRATIVE**:
```
• Executive & Admin Team
  - CEO, COO, CFO salaries
  - Admin staff
  - HR
• Legal & Compliance
  - Legal fees
  - Corporate filings
  - Compliance tools
• Accounting & Finance
  - Accounting services
  - Bookkeeping
  - Tax preparation
  - Finance software
• Insurance
  - D&O insurance
  - E&O insurance
  - General liability
  - Health insurance (employer portion)
• Office & Facilities
  - Rent and utilities
  - Office supplies
  - Furniture and equipment
• Business Software
  - Productivity tools (Slack, Zoom, Notion)
  - HR tools (Gusto, Rippling)
  - General business SaaS
• Bank Fees & Interest
  - Bank charges
  - Credit card processing (non-product)
  - Interest expense
```

## Categorization Rules & Best Practices

### Rule 1: Consistency is Key

**DO**:
- Use the same category for the same vendor every time
- Document category definitions and stick to them
- Review categorizations monthly for consistency

**DON'T**:
- Categorize AWS as both "Infrastructure" and "Development Tools"
- Switch between "Marketing" and "Advertising" for the same vendor
- Let different team members categorize the same expense type differently

### Rule 2: Follow Function, Not Department

Categorize based on what the expense does, not who requested it:

**Example**:
```
❌ WRONG: CEO bought AWS for the company → "G&A" (because CEO)
✅ RIGHT: AWS powers the product → "Infrastructure / COGS"

❌ WRONG: Marketing hired engineer contractor → "Marketing"
✅ RIGHT: Contractor built product features → "R&D / Engineering"
```

### Rule 3: Separate COGS from Operating Expenses

**COGS** = Costs that scale with customers/revenue:
- Hosting that grows with usage
- Payment processing (% of revenue)
- Customer support hours (if per-customer)

**Operating Expenses** = Fixed or growth-independent:
- Engineering salaries (same regardless of customer count)
- Office rent
- Marketing (acquiring customers, not serving them)

**Why it matters**: COGS is used to calculate gross margin, a key SaaS metric.

```
Gross Margin = (Revenue - COGS) / Revenue
Target: >70% for SaaS
```

### Rule 4: Capitalize vs Expense

Some costs should be **capitalized** (recorded as assets) rather than expensed immediately:

**Capitalize** (longer-term benefit):
- Equipment >$2,500 with multi-year life
- Software licenses (multi-year prepayment)
- Major improvements to leased space
- Internally-developed software (sometimes, consult accountant)

**Expense** (consumed immediately):
- Monthly subscriptions
- Salaries and wages
- Office supplies
- Marketing spend

**Consult your accountant** - capitalization rules vary by situation and accounting method (cash vs accrual).

### Rule 5: Multi-Use Vendor Splitting

Some vendors serve multiple purposes:

**Amazon**:
- Amazon Web Services (AWS) → Infrastructure / COGS
- Amazon.com (office supplies) → G&A / Office

**Solution**:
- Use transaction description and amount to differentiate
- AWS charges are typically >$100 and recurring
- Office supplies are typically <$200 and one-time

**Google**:
- Google Ads → Sales & Marketing / Advertising
- Google Workspace → G&A / Business Software
- Google Cloud Platform → Infrastructure / COGS

**Solution**:
- Vendor name often includes specific service
- "Google Ads" vs "Google Workspace" vs "GCP"

### Rule 6: Transfer vs Expense

**Transfers** (NOT expenses):
- Movements between your own bank accounts
- Owner investments or capital contributions
- Loan proceeds (not operating expense)
- Equity purchases

**Expenses** (actual spending):
- Payments to vendors for goods/services
- Payroll to employees
- Interest payments (on loans)
- Distributions to owners (for pass-through entities)

### Rule 7: Handling Refunds and Credits

**Refunds**:
- Net against the original expense category
- Don't create a separate "Refunds" category
- Update the month's total for that category

**Example**:
```
Jan AWS charge: +$2,800 (Infrastructure)
Feb AWS credit: -$500 (AWS refund)
Feb AWS charge: +$2,900

Net Feb Infrastructure (AWS): $2,400
Don't show: $2,900 expense + $500 "refund income"
```

## Common Categorization Challenges

### Challenge 1: Contractors vs Employees

**Question**: How to categorize contractors?

**Answer**: By function, not employment status:

```
Engineering Contractor → R&D / Contractors
Marketing Consultant → S&M / Marketing Contractors
Accounting Contractor → G&A / Accounting Services
```

**Why**:Allows apples-to-apples comparison of function costs regardless of employment type.

### Challenge 2: Mixed-Purpose Tools

**Question**: Slack is used by entire company - where to categorize?

**Answer**: Depends on primary use:

**Option A**: Allocate by user
```
- 10 users total
- 7 engineers, 2 marketing, 1 admin
- 70% → R&D, 20% → S&M, 10% → G&A
```

**Option B**: Simplify to primary function
```
- Primarily used for engineering coordination
- 100% → R&D / Development Tools
```

**Recommendation**: For startups, use Option B (simplify). Allocation is only worth it for very large expenses.

### Challenge 3: Founder Salaries

**Question**: Founders wear many hats - how to categorize salary?

**Answer**: By time allocation or primary role:

**Example**:
```
CEO/CTO spending:
- 60% engineering/product
- 30% fundraising/strategy
- 10% admin

Options:
1. Split: 60% R&D, 30% G&A, 10% G&A
2. Simplify: 100% R&D (if CTO role primary)

Recommendation: Simplify unless fundraising imminent (VCs care about "actual" vs "fully-loaded" burn)
```

### Challenge 4: One-Time vs Recurring

**Question**: Should I categorize differently based on frequency?

**Answer**: No - categorize by function, but FLAG unusual one-time items:

```
Normal Monthly Legal: $2,000 → G&A / Legal
One-Time Patent Filing: $15,000 → G&A / Legal (note: one-time)
```

**Why**: Keeps categories clean, but notation helps with burn rate calculations.

### Challenge 5: Customer vs Internal Use

**Question**: We use our own product - is it COGS or operating expense?

**Answer**: Internal use is operating expense, not COGS:

```
Hosting for customer-facing product: COGS / Infrastructure
Hosting for internal tools: R&D / Development Infrastructure
```

## SaaS-Specific Categorization

### Payment Processing Fees

**Categorization**: COGS (scales with revenue)

```
Stripe fees: 2.9% + $0.30 per transaction
Jan revenue: $25,000
Jan Stripe fees: ~$750

Category: COGS / Payment Processing
```

**Why**: Directly tied to delivering service to customers.

### Customer Success Team

**Pre-Product/Market Fit**: R&D (helping shape product)
**Post-PMF, High-Touch**: COGS (required to deliver value)
**Post-PMF, Low-Touch**: S&M (driving expansion/retention)

**Example**:
```
Early stage (seed): CS is product feedback → R&D
Series A+ enterprise: CS is required delivery → COGS
PLG motion: CS is upsell/expansion → S&M
```

### Infrastructure for Development

**Categorization**: R&D, not COGS

```
Production AWS (serves customers): COGS / Infrastructure
Development/Staging AWS: R&D / Development Tools
```

## Budget Allocation Benchmarks

Typical SaaS spend allocation by stage:

**Seed Stage** ($50K-150K/month burn):
```
R&D: 65-75% (building product)
S&M: 10-20% (early traction)
G&A: 10-15% (lean ops)
COGS: 5-10% (low revenue)
```

**Series A** ($150K-500K/month burn):
```
R&D: 50-60% (scaling product)
S&M: 25-35% (growth mode)
G&A: 8-12% (ops scaling)
COGS: 10-15% (revenue growing)
```

**Series B+** ($500K+/month burn):
```
R&D: 40-50% (mature product)
S&M: 35-45% (land grab)
G&A: 8-12% (efficient ops)
COGS: 10-15% (economies of scale)
```

**Rule of Thumb**: R&D should decline as % of spend while S&M increases post-PMF.

## Tools & Systems

### Chart of Accounts (CoA)

Your accounting system's CoA should mirror these categories:

```
5000 - Cost of Goods Sold
  5100 - Hosting & Infrastructure
  5200 - Payment Processing
  5300 - Third-Party Services

6000 - Research & Development
  6100 - Engineering Salaries
  6200 - Contractors
  6300 - Development Tools

7000 - Sales & Marketing
  7100 - Advertising
  7200 - Marketing Team
  7300 - Marketing Tools

8000 - General & Administrative
  8100 - Executive Team
  8200 - Legal & Compliance
  8300 - Accounting & Finance
  8400 - Insurance
  8500 - Office & Facilities
```

### Automation Tools

**Expense Management**:
- Ramp, Brex (auto-categorization + cards)
- Expensify, Divvy (receipt tracking)
- Mercury (banking + categorization)

**Accounting Software**:
- QuickBooks Online (standard)
- Xero (modern alternative)
- NetSuite (enterprise)

**Integration**:
- Auto-sync bank → accounting system
- Auto-categorization based on vendor
- Manual review for ambiguous items

## Monthly Reconciliation Process

1. **Export transactions** from Mercury/bank
2. **Auto-categorize** known vendors (90%)
3. **Manual review** ambiguous items (10%)
4. **Verify totals** by category
5. **Flag anomalies** (see anomaly-detection skill)
6. **Update budgets** if persistent changes
7. **Generate reports** (P&L, burn by category)

**Time commitment**: 2-4 hours/month for seed-stage startup

## Key Takeaways

1. **Consistency > Perfection** - It's more important to be consistent than to find the "perfect" category
2. **Function over Form** - Categorize by what the expense does, not who bought it
3. **Keep it Simple** - Don't over-complicate with too many categories
4. **Document Decisions** - Write down categorization rules for your company
5. **Review Regularly** - Monthly review catches errors early
6. **Automate What You Can** - Let software handle known vendors
7. **When in Doubt, Ask** - Consult your accountant for complex items

Proper expense categorization is the foundation of good financial management. Get it right and everything else (budgeting, forecasting, reporting) becomes much easier.
