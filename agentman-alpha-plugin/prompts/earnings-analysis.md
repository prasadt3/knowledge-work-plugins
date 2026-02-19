---
name: earnings-analysis
description: |
  Analyze a company's most recent earnings results by comparing current and prior period financials.
  Use after collecting data from run_equity_analysis_tool (for multi-year financials) and
  run_market_analysis_tool (for news context on earnings reaction). Produces a structured
  earnings review with beat/miss assessment, trend analysis, and forward outlook.
tools-required:
  - mcp__agentman-alpha__run_equity_analysis_tool
  - mcp__agentman-alpha__run_market_analysis_tool
estimated-time: 1-2 min
output-format: PDF or DOCX titled "Agentman — Earnings Analysis", authored by "Agentman Equity Research Assistant"
---

# Earnings Analysis

You are producing a structured analysis of a company's most recent earnings results. Focus on the delta between the latest period and prior periods, margin trends, and what the results signal for the future.

## Data Extraction

### From Equity Analysis Tool
- [ ] Revenue for last 4 fiscal years → compute YoY growth for each period
- [ ] Gross profit, operating income, net income for 4 years
- [ ] EPS for 4 years → compute YoY EPS growth
- [ ] Margins: gross, operating, net (compute for each year)
- [ ] Balance sheet: cash, debt, equity trends (2 years minimum)
- [ ] Cash flow: operating CF, FCF, CapEx, buybacks (2-3 years)
- [ ] Price performance: 1W, 1M, 3M returns (captures market reaction)

### From Market Analysis Tool
- [ ] Recent news headlines (look for earnings-related news)
- [ ] Analyst ratings and price target changes
- [ ] Current quote data

## Report Structure

### Header
```
# Agentman — Earnings Review: {Company Name} ({TICKER}) — FY{year}

**Reported**: {fiscal year end date} | **Price**: ${price}
**Analyst**: Agentman Equity Research Assistant
```

### Section 1: Headline Numbers
Present the most recent quarter/year in a highlight box format:

| Metric | FY{latest} | FY{prior} | YoY Change |
|--------|-----------|-----------|------------|
| **Revenue** | ${latest} | ${prior} | {+/-pct}% |
| **Gross Profit** | ${latest} | ${prior} | {+/-pct}% |
| **Operating Income** | ${latest} | ${prior} | {+/-pct}% |
| **Net Income** | ${latest} | ${prior} | {+/-pct}% |
| **EPS** | ${latest} | ${prior} | {+/-pct}% |

One-sentence verdict: "{Company} delivered {strong/mixed/weak} results with revenue {up/down} {X}% YoY and EPS {up/down} {X}% to ${eps}."

### Section 2: Revenue Analysis
- Absolute revenue and growth rate for the last 4 years
- Identify acceleration or deceleration pattern
- Comment on revenue quality (recurring vs. one-time, organic vs. acquisition-driven if known)
- Note any segment-level insights if available from your knowledge

### Section 3: Margin Trends
| Margin | FY-3 | FY-2 | FY-1 | FY0 | Trend |
|--------|------|------|------|-----|-------|
| Gross | ... | ... | ... | ... | Expanding/Compressing/Stable |
| Operating | ... | ... | ... | ... | ... |
| Net | ... | ... | ... | ... | ... |

Interpretation: What's driving margin changes? (Revenue mix shift, cost discipline, scale leverage, input costs, one-time items)

### Section 4: Balance Sheet Health
Compare the two most recent years:
| Metric | FY{latest} | FY{prior} | Change |
|--------|-----------|-----------|--------|
| Cash | ... | ... | ... |
| Total Debt | ... | ... | ... |
| Net Debt | ... | ... | ... |
| Equity | ... | ... | ... |
| Current Ratio | ... | ... | ... |

Assessment: Is the balance sheet strengthening or weakening? Note any major capital structure changes.

### Section 5: Cash Flow Quality
| Metric | FY-2 | FY-1 | FY0 |
|--------|------|------|-----|
| Operating CF | ... | ... | ... |
| CapEx | ... | ... | ... |
| Free Cash Flow | ... | ... | ... |
| Buybacks | ... | ... | ... |

Key question: Is FCF growing in line with earnings? If not, why? (Working capital changes, CapEx cycle, acquisition spending)

### Section 6: Market Reaction
- Stock performance since earnings (1W, 1M returns as proxy)
- Analyst sentiment: current consensus and any recent rating changes
- Price target context: where does the stock sit vs. analyst targets?

### Section 7: Forward Outlook

#### Positive Signals
3-4 bullets on what went right and what it implies going forward.

#### Concerns
2-3 bullets on what went wrong or what bears will focus on.

#### Key Questions for Next Quarter
3-4 specific questions investors should monitor:
- "{Specific question about a trend or metric}" — {why it matters}

### Disclaimer
> *This Agentman earnings analysis is for informational purposes only and does not constitute personalized investment advice. Past performance does not guarantee future results. Investors should conduct their own due diligence and consult a licensed financial advisor. Prepared by Agentman Equity Research Assistant.*

## Analysis Guidelines
- **Focus on the delta**: The most important information is what changed, not what stayed the same
- **Compute all YoY changes**: Never present raw numbers without context of growth/decline
- **Quality over quantity**: A 20% EPS beat driven by buybacks and tax rate is different from one driven by revenue growth
- **Cash flow matters**: Earnings can be managed; cash flow is harder to manipulate. Always check if FCF confirms the earnings story
- **Look for inflection points**: Is growth accelerating or decelerating? Are margins expanding or compressing? These trends matter more than the absolute numbers

## Brand Color Reference

All reports are output as **PDF or DOCX** (user's choice, PDF by default). Title: **"Agentman — Earnings Analysis"** (set in document metadata and cover page). Author: **Agentman Equity Research Assistant** (display in header/cover and footer). For DOCX, use `python-docx` with brand colors applied via `RGBColor`, table cell shading, and custom styles. Apply the Agentman brand palette from `references/brand-colors.md`, following the **agentman-pptx-style** design system.

- **Visual weight**: 70% Carbon/Charcoal, 20% Warm Neutrals, 10% Terracotta accent
- **Section titles**: `CHARCOAL_900` (#292322) with `AGENTMAN_500` (#CC785C) underline
- **Body text**: `CHARCOAL_950` (#141413); secondary `SLATE_600` (#475569)
- **Table headers**: `AGENTMAN_100` (#F6EAE6) light fill, `AGENTMAN_500` (#CC785C) terracotta text
- **Table borders**: `AGENTMAN_150` (#E3DACC) warm
- **Alternating table rows**: `AGENTMAN_50` (#FAF9F5) cream / white
- **Positive YoY changes** (growth, expansion): `AGENTMAN_500` (#CC785C) terracotta bold
- **Negative YoY changes** (decline, compression): `AGENTMAN_600` (#A65945) deep terracotta bold
- **Margin trend "Expanding"**: `AGENTMAN_500` terracotta; **"Compressing"**: `AGENTMAN_600` deep terracotta; **"Stable"**: `SLATE_600` (#475569)
- **Positive Signals section**: `AGENTMAN_500` terracotta accent
- **Concerns section**: `AGENTMAN_600` deep terracotta accent
- **Verdict text**: "strong results" `AGENTMAN_500`, "weak results" `AGENTMAN_600`, "mixed results" `CHARCOAL_950` bold

**BANNED**: Green, red, amber, blue (except ✓/✗ comparison symbols). No gradients. No invented colors. See `references/color-antipatterns.md`.
