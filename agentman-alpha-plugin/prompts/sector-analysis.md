---
name: sector-analysis
description: |
  Produce a sector-level analysis by comparing multiple representative companies within a sector.
  Use after collecting data from compare_stocks_tool for sector peers and optionally
  run_market_analysis_tool for the primary company. Produces sector landscape assessment
  with performance rankings, valuation spreads, and thematic trends.
tools-required:
  - mcp__agentman-alpha__compare_stocks_tool
  - mcp__agentman-alpha__run_market_analysis_tool (optional)
  - mcp__agentman-alpha__get_equity_snapshot_tool (optional)
estimated-time: 1-3 min
output-format: PDF or DOCX titled "Agentman — Sector Analysis", authored by "Agentman Equity Research Assistant"
---

# Sector Analysis

You are producing a sector-level analysis using data from representative companies. The goal is to assess the sector's health, identify leaders and laggards, and surface investment themes.

## Preparation

### Identify Sector Representatives
If the user specifies a sector but not tickers, select 3-5 representative companies:
- **Technology**: AAPL, MSFT, GOOGL, NVDA, META
- **Semiconductors**: NVDA, AMD, INTC, AVGO, QCOM
- **Cloud/SaaS**: MSFT, CRM, NOW, SNOW, DDOG
- **E-Commerce**: AMZN, SHOP, MELI, SE, EBAY
- **Financials**: JPM, BAC, GS, MS, WFC
- **Healthcare**: UNH, JNJ, LLY, PFE, ABBV
- **Energy**: XOM, CVX, COP, SLB, EOG
- **Consumer Discretionary**: AMZN, TSLA, HD, NKE, MCD
- **Industrials**: CAT, HON, UNP, GE, DE
- **Communication**: GOOGL, META, DIS, NFLX, T

Use `compare_stocks_tool` with the selected tickers (max 5).

## Report Structure

### Header
```
# Agentman — Sector Analysis: {Sector Name}

**Date**: {date} | **Companies Analyzed**: {TICK1}, {TICK2}, {TICK3}, ...
**Analyst**: Agentman Equity Research Assistant
```

### Section 1: Sector Snapshot
Brief 2-3 sentence overview:
- Current sector narrative (what's driving the sector right now)
- General direction (expanding, contracting, rotating)
- Key macro factor influencing the sector

### Section 2: Performance Scorecard
| Company | Price | 1M Return | 3M Return | % from High | Volatility |
|---------|-------|-----------|-----------|-------------|------------|
| ... | ... | ... | ... | ... | ... |

**Sector Leader**: {TICKER} — {why}
**Sector Laggard**: {TICKER} — {why}

### Section 3: Valuation Landscape
| Company | P/B | P/S | EV/EBITDA | Div. Yield |
|---------|-----|-----|-----------|------------|
| ... | ... | ... | ... | ... |
| **Sector Avg** | ... | ... | ... | ... |

Compute sector averages. Identify:
- **Cheapest on EV/EBITDA**: {TICKER} at {X}x
- **Most Expensive**: {TICKER} at {X}x
- **Valuation Spread**: {X}x range — {wide spread = dispersion of expectations / narrow = consensus}

### Section 4: Profitability Comparison
| Company | Gross Margin | Operating Margin | Net Margin |
|---------|-------------|-----------------|------------|
| ... | ... | ... | ... |
| **Sector Avg** | ... | ... | ... |

Identify the margin leader and discuss why (business model, scale, mix, pricing power).

### Section 5: Analyst Sentiment Across Sector
| Company | Consensus | Median PT | Implied Upside |
|---------|-----------|-----------|----------------|
| ... | ... | ... | ... |

Overall sector sentiment: Are analysts broadly bullish, mixed, or cautious? Which stock has the most/least upside?

### Section 6: Sector Themes & Catalysts

#### Tailwinds (Positive)
3-4 sector-level tailwinds:
- **{Theme}**: 1-sentence explanation of the trend and which companies benefit most

#### Headwinds (Negative)
2-3 sector-level headwinds:
- **{Theme}**: 1-sentence explanation and which companies are most exposed

#### Key Catalysts to Watch
3-4 upcoming events or data points that could move the sector:
- {Event/date/data point} — {expected impact}

### Section 7: Sector Positioning Recommendations

#### Best Positioned
1-2 companies with strongest sector positioning. Explain why (valuation + momentum + fundamentals alignment).

#### Potential Value
1-2 companies trading at a discount to sector peers that could be turnaround candidates. Explain the thesis and the risk.

#### Proceed with Caution
1 company where risk/reward is least favorable. Explain why.

### Disclaimer
> *This Agentman sector analysis is for informational purposes only and does not constitute personalized investment advice. Past performance does not guarantee future results. Investors should conduct their own due diligence and consult a licensed financial advisor. Prepared by Agentman Equity Research Assistant.*

## Analysis Guidelines
- Think at the sector level first, then drill into individual companies
- Always compute and show sector averages for key metrics
- Identify dispersion: a sector where all stocks move together tells a different story than one with wide performance gaps
- Connect macro factors to sector dynamics (e.g., rising rates → bank margins, AI spending → semiconductor demand)
- Use relative metrics (vs. sector average) not just absolute values

## Brand Color Reference

All reports are output as **PDF or DOCX** (user's choice, PDF by default). Title: **"Agentman — Sector Analysis"** (set in document metadata and cover page). Author: **Agentman Equity Research Assistant** (display in header/cover and footer). For DOCX, use `python-docx` with brand colors applied via `RGBColor`, table cell shading, and custom styles. Apply the Agentman brand palette from `references/brand-colors.md`, following the **agentman-pptx-style** design system.

- **Visual weight**: 70% Carbon/Charcoal, 20% Warm Neutrals, 10% Terracotta accent
- **Section titles**: `CHARCOAL_900` (#292322) with `AGENTMAN_500` (#CC785C) underline
- **Body text**: `CHARCOAL_950` (#141413); secondary `SLATE_600` (#475569)
- **Table headers**: `AGENTMAN_100` (#F6EAE6) light fill, `AGENTMAN_500` (#CC785C) terracotta text
- **Table borders**: `AGENTMAN_150` (#E3DACC) warm
- **Alternating table rows**: `AGENTMAN_50` (#FAF9F5) cream / white
- **Sector Average row**: `AGENTMAN_75` (#F0EEE6) warm cream highlight
- **Sector Leader / best values**: `AGENTMAN_500` (#CC785C) terracotta bold
- **Sector Laggard / worst values**: `AGENTMAN_600` (#A65945) deep terracotta
- **Tailwinds (Positive)**: `AGENTMAN_500` terracotta accent
- **Headwinds (Negative)**: `AGENTMAN_600` deep terracotta accent
- **"Best Positioned"**: `AGENTMAN_500` terracotta; **"Proceed with Caution"**: `AGENTMAN_600` deep terracotta; **"Potential Value"**: `AGENTMAN_400` (#D97757) highlight

**BANNED**: Green, red, amber, blue (except ✓/✗ comparison symbols). No gradients. No invented colors. See `references/color-antipatterns.md`.
