---
name: portfolio-review
description: |
  Analyze a multi-stock portfolio for diversification, risk, relative performance, and rebalancing
  opportunities. Use after collecting data from compare_stocks_tool and get_equity_snapshot_tool
  for each holding. Produces a portfolio health assessment with allocation analysis and action items.
tools-required:
  - mcp__agentman-alpha__compare_stocks_tool
  - mcp__agentman-alpha__get_equity_snapshot_tool
estimated-time: 1-3 min
output-format: PDF or DOCX titled "Agentman — Portfolio Review", authored by "Agentman Equity Research Assistant"
---

# Portfolio Review

You are producing a portfolio-level analysis for a user's holdings. Focus on diversification, risk concentration, relative performance, and actionable rebalancing insights.

## Data Collection Strategy

1. Run `compare_stocks_tool` with all holdings (up to 5 at a time)
2. Run `get_equity_snapshot_tool` on each holding for detailed metrics
3. If portfolio has more than 5 holdings, run multiple comparison batches

## Data Extraction

For each holding, extract:
- [ ] Price, market cap, sector, industry
- [ ] P/E, P/B, EV/EBITDA
- [ ] Gross margin, operating margin, net margin
- [ ] Dividend yield
- [ ] 1M, 3M returns, volatility
- [ ] Beta
- [ ] Analyst consensus, median price target, implied upside
- [ ] % from 52-week high

## Report Structure

### Header
```
# Agentman — Portfolio Review

**Date**: {date} | **Holdings**: {count} stocks | **Sectors**: {count} sectors
**Analyst**: Agentman Equity Research Assistant
```

### Section 1: Portfolio Overview

#### Holdings Summary
| # | Ticker | Company | Sector | Price | Mkt Cap |
|---|--------|---------|--------|-------|---------|
| 1 | ... | ... | ... | ... | ... |

#### Sector Exposure
| Sector | Holdings | Tickers |
|--------|----------|---------|
| Technology | {count} | {list} |
| Healthcare | {count} | {list} |
| ... | ... | ... |

Flag concentration risk: if >50% of holdings are in one sector, or if >3 holdings are in the same industry.

### Section 2: Performance Dashboard
| Ticker | 1M Return | 3M Return | % from High | Volatility | Beta |
|--------|-----------|-----------|-------------|------------|------|
| ... | ... | ... | ... | ... | ... |
| **Portfolio Avg** | ... | ... | ... | ... | ... |

Identify:
- **Best Performer**: {TICKER} — {return} over {period}
- **Worst Performer**: {TICKER} — {return} over {period}
- **Most Volatile**: {TICKER} — {volatility}%
- **Portfolio Beta**: {weighted average if weights provided, simple average otherwise}

### Section 3: Valuation Comparison
| Ticker | P/E | P/B | EV/EBITDA | Div. Yield | Analyst Upside |
|--------|-----|-----|-----------|------------|----------------|
| ... | ... | ... | ... | ... | ... |
| **Portfolio Avg** | ... | ... | ... | ... | ... |

Identify:
- **Cheapest**: {TICKER} on {metric}
- **Most Expensive**: {TICKER} on {metric}
- **Highest Analyst Upside**: {TICKER} at {pct}%
- **Highest Yield**: {TICKER} at {pct}%

### Section 4: Profitability Quality
| Ticker | Gross Margin | Operating Margin | Net Margin |
|--------|-------------|-----------------|------------|
| ... | ... | ... | ... |
| **Portfolio Avg** | ... | ... | ... |

Assess overall portfolio quality: Are these high-margin businesses? Any weak links?

### Section 5: Analyst Sentiment
| Ticker | Consensus | Buy | Hold | Sell | Median PT | Upside |
|--------|-----------|-----|------|------|-----------|--------|
| ... | ... | ... | ... | ... | ... | ... |

Overall portfolio sentiment: How many holdings have Buy consensus? Any with Sell ratings? Average implied upside.

### Section 6: Risk Assessment

#### Concentration Risk
- Sector concentration: {assessment}
- Single-stock concentration: {assessment if weights known}
- Geographic concentration: {assessment based on company profiles}

#### Correlation Risk
- Identify holdings likely to be highly correlated (same sector, similar business models)
- Note diversification gaps (e.g., no defensive holdings, no international exposure)

#### Volatility Profile
- Average portfolio volatility: {pct}%
- Average beta: {value}
- Interpretation: This portfolio is {more/less} volatile than the market

### Section 7: Action Items

Prioritized list of 3-5 specific, actionable recommendations:

1. **{Action}**: {Explanation with supporting data}
   - *Priority*: {High/Medium/Low}
   - *Rationale*: {Why this matters}

Categories of actions to consider:
- **Rebalancing**: Over-concentrated sectors or correlated positions
- **Valuation**: Holdings trading significantly above/below analyst targets
- **Quality**: Holdings with weak margins or deteriorating fundamentals
- **Risk reduction**: Reducing exposure to highest-volatility or highest-beta positions
- **Income**: Adding or reducing dividend exposure
- **Diversification**: Gaps in sector, geography, or style coverage

### Portfolio Profile Alignment

Assess how the overall portfolio aligns with each investor profile:

#### Per-Holding Profile Fit
| Ticker | Best Profile Fit | Conservative | Moderate | Aggressive | Key Factor |
|--------|-----------------|-------------|----------|------------|------------|
| ... | {profile} | {Good/Moderate/Poor} | {Good/Moderate/Poor} | {Good/Moderate/Poor} | {key metric} |

#### Portfolio-Level Assessment
| Profile | Holdings That Fit | Holdings That Don't | Portfolio Alignment |
|---------|------------------|--------------------|--------------------|
| **Conservative** | {list} | {list} | {Strong/Moderate/Weak} |
| **Moderate** | {list} | {list} | {Strong/Moderate/Weak} |
| **Aggressive** | {list} | {list} | {Strong/Moderate/Weak} |

**Portfolio's Natural Profile**: Based on average beta ({value}), average dividend yield ({value}%), and growth characteristics, this portfolio most closely aligns with a **{profile}** investor profile.

If the portfolio's natural profile differs from the user's stated preference, flag misaligned holdings and suggest adjustments.

### Disclaimer
> *This Agentman portfolio review is for informational purposes only and does not constitute personalized investment advice. Past performance does not guarantee future results. Investors should conduct their own due diligence and consult a licensed financial advisor. Prepared by Agentman Equity Research Assistant.*

## Analysis Guidelines
- If the user provides portfolio weights, use weighted metrics. Otherwise, use equal-weight averages.
- Always flag concentration risk — most retail portfolios are under-diversified
- Frame action items as considerations, not directives
- Think about what's missing from the portfolio, not just what's in it
- Compare portfolio averages to broad market benchmarks when possible (e.g., S&P 500 P/E ~20-22x, yield ~1.3%)

## Brand Color Reference

All reports are output as **PDF or DOCX** (user's choice, PDF by default). Title: **"Agentman — Portfolio Review"** (set in document metadata and cover page). Author: **Agentman Equity Research Assistant** (display in header/cover and footer). For DOCX, use `python-docx` with brand colors applied via `RGBColor`, table cell shading, and custom styles. Apply the Agentman brand palette from `references/brand-colors.md`, following the **agentman-pptx-style** design system.

- **Visual weight**: 70% Carbon/Charcoal, 20% Warm Neutrals, 10% Terracotta accent
- **Section titles**: `CHARCOAL_900` (#292322) with `AGENTMAN_500` (#CC785C) underline
- **Body text**: `CHARCOAL_950` (#141413); secondary `SLATE_600` (#475569)
- **Table headers**: `AGENTMAN_100` (#F6EAE6) light fill, `AGENTMAN_500` (#CC785C) terracotta text
- **Table borders**: `AGENTMAN_150` (#E3DACC) warm
- **Alternating table rows**: `AGENTMAN_50` (#FAF9F5) cream / white
- **Best Performer / positive returns**: `AGENTMAN_500` (#CC785C) terracotta bold
- **Worst Performer / negative returns**: `AGENTMAN_600` (#A65945) deep terracotta bold
- **Portfolio Average row**: `AGENTMAN_75` (#F0EEE6) warm cream highlight
- **Action item priority**: High = `AGENTMAN_600` deep terracotta bold; Medium = `AGENTMAN_400` (#D97757) highlight; Low = `CHARCOAL_950` bold
- **Profile alignment**: "Strong" = `AGENTMAN_500` terracotta; "Moderate" = `CHARCOAL_950` bold; "Weak" = `AGENTMAN_600` deep terracotta
- **Concentration risk flags**: `AGENTMAN_600` deep terracotta for high, `AGENTMAN_400` warm highlight for moderate

**BANNED**: Green, red, amber, blue (except ✓/✗ comparison symbols). No gradients. No invented colors. See `references/color-antipatterns.md`.
