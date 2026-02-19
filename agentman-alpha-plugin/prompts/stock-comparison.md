---
name: stock-comparison
description: |
  Build a structured side-by-side stock comparison with rankings and relative value analysis.
  Use after collecting data from compare_stocks_tool and optionally get_equity_snapshot_tool
  for 2-5 tickers. Produces a comparison report with metrics tables and actionable takeaways.
tools-required:
  - mcp__agentman-alpha__compare_stocks_tool
  - mcp__agentman-alpha__get_equity_snapshot_tool (optional, for enrichment)
estimated-time: 1-2 min
output-format: PDF or DOCX titled "Agentman — Stock Comparison Analysis", authored by "Agentman Equity Research Assistant"
---

# Stock Comparison Analysis

You are producing a side-by-side comparison of 2-5 stocks. You have data from `compare_stocks_tool` and optionally `get_equity_snapshot_tool` for additional context.

## Data Extraction Checklist

For each stock, extract:
- [ ] Price, market cap
- [ ] P/B, P/S, EV/EBITDA
- [ ] Gross margin, operating margin, net margin
- [ ] Dividend yield
- [ ] 1M, 3M returns
- [ ] Volatility
- [ ] Analyst consensus, average price target
- [ ] Beta
- [ ] Current ratio (if available)
- [ ] % from 52-week high (if available from snapshots)

Compute:
- [ ] P/E from price / EPS if EPS available
- [ ] Implied upside/downside to analyst median price target

## Report Structure

### Header
```
# Agentman — {Category} Comparison: {TICKER1} vs. {TICKER2} vs. ...

**Date**: {date}
**Analyst**: Agentman Equity Research Assistant
```

### Section 1: At a Glance
Overview table with company-level facts:
| Metric | TICK1 | TICK2 | TICK3 | ... |
|--------|-------|-------|-------|-----|
| **Price** | ... | ... | ... | |
| **Market Cap** | ... | ... | ... | |
| **Industry** | ... | ... | ... | |
| **Employees** | ... | ... | ... | |
| **Beta** | ... | ... | ... | |

### Section 2: Valuation
| Metric | TICK1 | TICK2 | TICK3 | Edge |
|--------|-------|-------|-------|------|
| P/B | ... | ... | ... | Lowest wins |
| P/S | ... | ... | ... | Lowest wins |
| EV/EBITDA | ... | ... | ... | Lowest wins |
| Dividend Yield | ... | ... | ... | Highest wins |

Add an "Edge" column identifying the winner for each metric. Follow with a 2-3 sentence interpretation paragraph explaining the valuation landscape.

### Section 3: Profitability
| Metric | TICK1 | TICK2 | TICK3 | Edge |
|--------|-------|-------|-------|------|
| Gross Margin | ... | ... | ... | Highest wins |
| Operating Margin | ... | ... | ... | Highest wins |
| Net Margin | ... | ... | ... | Highest wins |

Interpretation paragraph: explain why margins differ (business model, revenue mix, scale).

### Section 4: Financial Health
| Metric | TICK1 | TICK2 | TICK3 | Edge |
|--------|-------|-------|-------|------|
| Current Ratio | ... | ... | ... | Highest wins |

Brief interpretation. Note if a low current ratio is by design (e.g., Apple's buyback strategy).

### Section 5: Price Performance
| Period | TICK1 | TICK2 | TICK3 | Edge |
|--------|-------|-------|-------|------|
| 1 Week | ... | ... | ... | Best wins |
| 1 Month | ... | ... | ... | Best wins |
| 3 Months | ... | ... | ... | Best wins |
| % from 52-Wk High | ... | ... | ... | Closest wins |
| Volatility | ... | ... | ... | Lowest wins |

Interpretation: identify momentum leader, biggest pullback (potential opportunity), risk profiles.

### Section 6: Analyst Sentiment
| Metric | TICK1 | TICK2 | TICK3 |
|--------|-------|-------|-------|
| Consensus | ... | ... | ... |
| Buy + Strong Buy | ... | ... | ... |
| Hold | ... | ... | ... |
| Sell | ... | ... | ... |
| Median PT | ... | ... | ... |
| Implied Upside | ... | ... | ... |

Highlight the stock with the most analyst upside and the strongest buy conviction.

### Section 7: Relative Value Summary
Winner-by-category table:
| Dimension | Winner | Why |
|-----------|--------|-----|
| Cheapest Valuation | ... | Key metric cited |
| Best Margins | ... | Key metric cited |
| Strongest Balance Sheet | ... | Key metric cited |
| Best Momentum | ... | Key metric cited |
| Lowest Volatility | ... | Key metric cited |
| Most Analyst Upside | ... | Key metric cited |
| Best Income | ... | Key metric cited |

### Section 8: Key Takeaways
Numbered list with 3-5 takeaways, one per stock being compared. Each takeaway:
1. **{TICKER} is the {characterization} play.** 2-3 sentences explaining the investment angle, who it's best for, and the primary risk.

### Section 9: Investor Profile Fit

For each compared stock, indicate which investor profile it best suits using available metrics (beta, dividend yield, P/E, growth, momentum):

| Ticker | Best Profile Fit | Conservative | Moderate | Aggressive | Key Factor |
|--------|-----------------|-------------|----------|------------|------------|
| TICK1 | {profile} | {Good/Moderate/Poor} | {Good/Moderate/Poor} | {Good/Moderate/Poor} | {e.g., "Low beta + 3.2% yield"} |
| TICK2 | {profile} | {Good/Moderate/Poor} | {Good/Moderate/Poor} | {Good/Moderate/Poor} | {e.g., "PEG 1.2, strong ROE"} |
| ... | ... | ... | ... | ... | ... |

**Profile-Based Pick**:
- **Conservative pick**: {TICKER} — {1-sentence why: yield, stability, margin of safety}
- **Moderate pick**: {TICKER} — {1-sentence why: growth-value balance, analyst consensus}
- **Aggressive pick**: {TICKER} — {1-sentence why: growth rate, momentum, upside}

Final paragraph with a "For new money today" recommendation framed as considerations, not advice.

### Disclaimer
> *This Agentman comparison report is for informational purposes only and does not constitute personalized investment advice. Past performance does not guarantee future results. Investors should conduct their own due diligence and consult a licensed financial advisor. Prepared by Agentman Equity Research Assistant.*

## Formatting Rules
- Always bold the "winner" value in each row of comparison tables
- Use the "Edge" column consistently to highlight the best-in-class for each metric
- Keep interpretation paragraphs to 2-3 sentences
- If a metric is unavailable for a stock, show "N/A" rather than omitting the row

## Brand Color Reference

All reports are output as **PDF or DOCX** (user's choice, PDF by default). Title: **"Agentman — Stock Comparison Analysis"** (set in document metadata and cover page). Author: **Agentman Equity Research Assistant** (display in header/cover and footer). For DOCX, use `python-docx` with brand colors applied via `RGBColor`, table cell shading, and custom styles. Apply the Agentman brand palette from `references/brand-colors.md`, following the **agentman-pptx-style** design system.

- **Visual weight**: 70% Carbon/Charcoal, 20% Warm Neutrals, 10% Terracotta accent
- **Section titles**: `CHARCOAL_900` (#292322) with `AGENTMAN_500` (#CC785C) underline
- **Body text**: `CHARCOAL_950` (#141413); secondary `SLATE_600` (#475569)
- **Table headers**: `AGENTMAN_100` (#F6EAE6) light fill, `AGENTMAN_500` (#CC785C) terracotta text
- **Table borders**: `AGENTMAN_150` (#E3DACC) warm
- **Alternating table rows**: `AGENTMAN_50` (#FAF9F5) cream / white
- **"Edge" / winner values**: `AGENTMAN_500` (#CC785C) terracotta bold to highlight best-in-class
- **Worst-in-class values**: `AGENTMAN_600` (#A65945) deep terracotta
- **Profile-Based Pick labels**: Conservative in `SLATE_700` (#334155), Moderate in `AGENTMAN_700` (#8B4A38), Aggressive in `AGENTMAN_500` (#CC785C)
- **Terracotta budget**: max 3 `AGENTMAN_500` elements per section

**BANNED**: Green, red, amber, blue (except ✓/✗ comparison symbols). No gradients. No invented colors. See `references/color-antipatterns.md`.
