---
name: comprehensive-equity-report
description: |
  Synthesize multi-tool data into an institutional-quality equity research report. Use this prompt
  after collecting data from run_equity_analysis_tool, run_market_analysis_tool, and get_valuation_tool
  for a single ticker. Produces an 8-section report with executive summary through appendix.
tools-required:
  - mcp__agentman-alpha__run_equity_analysis_tool
  - mcp__agentman-alpha__run_market_analysis_tool
  - mcp__agentman-alpha__get_valuation_tool
estimated-time: 4-6 min
output-format: PDF or DOCX titled "Agentman — {Report Title}", authored by "Agentman Equity Research Assistant"
---

# Comprehensive Equity Research Report

You are producing an institutional-quality equity research report. You have collected data from three sources:
1. **Equity Analysis** (`run_equity_analysis_tool`) — financials, ratios, price history
2. **Market Analysis** (`run_market_analysis_tool`) — profile, quote, news, analyst ratings
3. **DCF Valuation** (`get_valuation_tool`) — Damodaran intrinsic value estimate

## Data Extraction Checklist

Before writing, extract and compute these values from the raw data:

### From Equity Analysis + Market Analysis
- [ ] Current price, daily change, 52-week range
- [ ] Market cap
- [ ] Revenue for last 4 fiscal years → compute YoY growth rates
- [ ] Gross profit, operating income, net income for last 4 years
- [ ] EPS for last 4 years
- [ ] Gross margin, operating margin, net margin
- [ ] P/E (compute: price / TTM EPS), P/B, P/S, EV/EBITDA
- [ ] Balance sheet: total assets, equity, cash, total debt, net debt (2 years for trend)
- [ ] Cash flow: operating CF, CapEx, FCF, buybacks (2-3 years)
- [ ] Analyst ratings: buy/hold/sell counts, consensus, price targets (avg, median, high, low)
- [ ] Price performance: 1W, 1M, 3M, 6M, 1Y returns
- [ ] 50-day and 200-day moving averages
- [ ] Volatility and beta

### From DCF Valuation
- [ ] Estimated intrinsic value per share
- [ ] Price as percentage of intrinsic value
- [ ] Key assumptions: revenue growth rate, 5Y CAGR, operating margin, target margin, convergence years, sales/capital ratios
- [ ] Industry classification used

## Report Structure

### Header — CRITICAL: Agentman Branding Required

The first line of every report MUST begin with "Agentman —". This is the product brand and must ALWAYS appear as the title prefix. The analyst line MUST read "Equity Research Assistant". Never omit either element.

```
# Agentman — Comprehensive Equity Research Report: {Company Name} ({TICKER})

**Date**: {date} | **Price**: ${price} | **Market Cap**: ${market_cap}
**Analyst**: Equity Research Assistant
```

When generating the PDF/DOCX, the page 1 title MUST render as:
- **Title line**: "Agentman — Comprehensive Equity Research Report: {Company Name} ({TICKER})"
- **Subtitle/analyst line**: "Equity Research Assistant | {date}"
- Set document metadata title to "Agentman — Comprehensive Equity Research Report: {Company Name} ({TICKER})"
- Set document metadata author to "Agentman Equity Research Assistant"

Do NOT omit "Agentman —" from the title. Do NOT use only the company name as the title.

### Section 1: Executive Summary (3-5 sentences)
- State the investment thesis in one sentence
- Highlight the most important financial result (e.g., record revenue, margin expansion)
- Note the stock's position relative to 52-week range and analyst targets
- Mention the DCF valuation finding with appropriate context
- End with a balanced forward-looking statement

### Section 2: Company Overview
Present as a key-facts table:
| Field | Value |
|-------|-------|
| CEO | ... |
| Sector / Industry | ... |
| Employees | ... |
| Headquarters | ... |
| Beta | ... |

Follow with a 2-3 sentence business description focusing on revenue segments and competitive positioning.

### Section 3: Financial Analysis

#### Revenue & Profitability Table
| Metric | FY-3 | FY-2 | FY-1 | FY0 (Latest) |
|--------|------|------|------|---------------|
| Revenue | ... | ... | ... | ... |
| YoY Growth | ... | ... | ... | ... |
| Gross Profit | ... | ... | ... | ... |
| Operating Income | ... | ... | ... | ... |
| Net Income | ... | ... | ... | ... |
| EPS | ... | ... | ... | ... |

Include a "Key takeaway" paragraph interpreting the trends (growth acceleration/deceleration, margin expansion/compression, what's driving changes).

#### Balance Sheet Table (2-year comparison)
Highlight: assets, equity, cash, debt, net debt, current ratio. Note improvement or deterioration.

#### Cash Flow & Capital Allocation Table (2-3 years)
Highlight: operating CF, CapEx, FCF, buybacks. Note capital allocation philosophy.

### Section 4: Valuation

#### Market Multiples Table
| Multiple | Value | Context |
|----------|-------|---------|
| P/E (TTM) | ... | Compute from price/EPS |
| P/S | ... | Note vs. S&P average |
| P/B | ... | Note if distorted by buybacks |
| EV/EBITDA | ... | ... |
| Dividend Yield | ... | ... |

#### DCF Intrinsic Value Table
| Parameter | Value |
|-----------|-------|
| Estimated Intrinsic Value | ... |
| Current Price | ... |
| Price as % of Value | ... |
| 5-Year Revenue CAGR | ... |
| Target Operating Margin | ... |

Follow with interpretation:
1. State the headline finding (e.g., "trading at Nx intrinsic value")
2. List 3-4 caveats about why the DCF may undervalue/overvalue the company
3. Provide a balanced interpretation of what the market is pricing in

### Section 4.5: Advanced Valuation (Optional)

Include this section when Comparable Company Analysis and/or Merton Model data has been collected (e.g., via `/advanced-valuation` or when the research plan includes comps/Merton steps). Skip if only DCF data is available.

#### Comparable Company Analysis (if comps data collected)
| Multiple | Target | Peer Median | Implied Value | Weight |
|----------|--------|-------------|---------------|--------|
| P/E | ... | ... | ${implied} | {w}% |
| EV/EBITDA | ... | ... | ${implied} | {w}% |
| P/S | ... | ... | ${implied} | {w}% |
| P/B | ... | ... | ${implied} | {w}% |
| **Weighted Fair Value** | — | — | **${fair_value}** | **100%** |

**Fair Value Range**: ${low} (P25) to ${high} (P75)
**Peer Group**: {list peers used}

Follow with 1-2 sentences on whether the stock appears cheap or expensive relative to peers and which multiple is most informative.

#### Merton Model (if Merton data collected)
| Metric | Value |
|--------|-------|
| Merton Equity Value (per share) | ${merton_val} |
| Current Price | ${price} |
| Distance to Default | {d2} |
| Implied Default Probability | {pct}% |

Follow with 1-2 sentences on what the Merton Model implies about leverage risk and whether the market is appropriately pricing default risk.

#### Valuation Synthesis (if multiple methodologies available)
| Methodology | Implied Value | vs. Market Price |
|-------------|---------------|------------------|
| DCF (Damodaran) | ${dcf_val} | {+/-pct}% |
| Comps (Weighted) | ${comps_val} | {+/-pct}% |
| Merton Model | ${merton_val} | {+/-pct}% |

**Consensus Range**: ${low} to ${high}

Note convergence or divergence across methodologies and what that implies about valuation confidence.

### Section 5: Analyst Sentiment
- Ratings breakdown table (Strong Buy through Strong Sell + consensus)
- Price target table (High, Median, Average, Low + implied return from current price)
- 1-2 sentence interpretation

### Section 6: Price Performance
| Period | Return |
|--------|--------|
| 1 Week | ... |
| 1 Month | ... |
| 3 Months | ... |
| 6 Months | ... |
| 1 Year | ... |

Note position vs. 50-day and 200-day MAs. Comment on trend direction and momentum.

### Section 7: Risk Analysis

#### Bull Case (3-5 bullets)
Each bullet: **Bold label** followed by 1-sentence explanation with specific data.

#### Bear Case (3-5 bullets)
Same format. Cover: valuation risk, concentration risk, competitive risk, macro/regulatory risk, execution risk.

### Section 8: Investment Conclusion
- 2-3 paragraph synthesis
- Never give a specific buy/sell rating — frame as considerations

### Section 8.5: Investor Profile Suitability

Score the stock across three investor profiles using the investor-profile-methodology skill rubric (50 points each):

#### Profile Scores
| Profile | Score | Rating | Verdict |
|---------|-------|--------|---------|
| **Conservative** | {X}/50 | {Excellent/Good/Moderate/Poor Fit} | {1-sentence: suitable for income/stability? Key factor.} |
| **Moderate** | {X}/50 | {Excellent/Good/Moderate/Poor Fit} | {1-sentence: balanced growth-value? Key factor.} |
| **Aggressive** | {X}/50 | {Excellent/Good/Moderate/Poor Fit} | {1-sentence: growth/momentum play? Key factor.} |

**Best Fit**: {profile name} — {1-sentence rationale citing the strongest scoring criterion}

#### Profile-Specific Guidance
- **Conservative investors**: {2 sentences — position sizing, entry condition, key risk}
- **Moderate investors**: {2 sentences — position sizing, what to watch, time horizon}
- **Aggressive investors**: {2 sentences — position sizing, catalyst, upside target}

Use data already extracted in Sections 3-7 to compute scores. Reference the investor-profile-methodology skill for threshold tables.

### Appendix: Key Data Summary
Single table with the 12-15 most important metrics for quick reference.

### Disclaimer
Always end with:
> *This Agentman research report is for informational purposes only and does not constitute personalized investment advice. Past performance does not guarantee future results. Investors should conduct their own due diligence and consult a licensed financial advisor. Prepared by Agentman Equity Research Assistant.*

## Formatting Rules
- Use `$` for all currency values, `B` for billions, `T` for trillions
- Round percentages to 1 decimal place
- Use markdown tables for all structured data
- Bold the most important numbers in narrative text
- Use horizontal rules (`---`) between major sections
- Keep paragraphs to 3-4 sentences maximum

## Brand Color Reference

All reports are output as **PDF or DOCX** (user's choice, PDF by default). Title: **"Agentman — {Report Title}"** (set in document metadata and cover page). Author: **Agentman Equity Research Assistant** (display in header/cover and footer). For DOCX, use `python-docx` with brand colors applied via `RGBColor`, table cell shading, and custom styles. Apply the Agentman brand palette from `references/brand-colors.md`, following the **agentman-pptx-style** design system. Quiet confidence — charcoal suits, not fire trucks.

- **Visual weight**: 70% Carbon/Charcoal, 20% Warm Neutrals, 10% Terracotta accent
- **Section titles**: `CHARCOAL_900` (#292322) with `AGENTMAN_500` (#CC785C) underline
- **Body text**: `CHARCOAL_950` (#141413); secondary `SLATE_600` (#475569)
- **Table headers**: `AGENTMAN_100` (#F6EAE6) light fill, `AGENTMAN_500` (#CC785C) terracotta text
- **Table borders**: `AGENTMAN_150` (#E3DACC) warm
- **Alternating rows**: `AGENTMAN_50` (#FAF9F5) cream / white
- **Highlight rows**: `AGENTMAN_75` (#F0EEE6) warm cream
- **Cover page**: title in `CHARCOAL_900`, accent in `AGENTMAN_700` (#8B4A38)
- **Header/footer**: `SLATE_500` (#64748B) text, `AGENTMAN_500` (#CC785C) rule
- **Positive emphasis** (gains, upside, bullish): `AGENTMAN_500` (#CC785C) terracotta bold
- **Negative emphasis** (losses, downside, bearish): `AGENTMAN_600` (#A65945) deep terracotta bold
- **Caution/highlight**: `AGENTMAN_400` (#D97757) warm highlight
- **Verdict/callout boxes**: `AGENTMAN_75` (#F0EEE6) cream bg + `CHARCOAL_950` heading. Or `AGENTMAN_500` border + `AGENTMAN_50` cream bg.
- **Badges**: `AGENTMAN_100` bg + `AGENTMAN_800` text + `AGENTMAN_200` border. No color-coded tiers.
- **Terracotta budget**: max 3 `AGENTMAN_500` elements per section

**BANNED**: Green, red, amber, blue (except ✓/✗ comparison symbols). No gradients. No invented colors. See `references/color-antipatterns.md`.
