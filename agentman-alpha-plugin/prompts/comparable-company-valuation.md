---
name: comparable-company-valuation
description: |
  Perform a Comparable Company Analysis (Comps) to derive an implied fair value range from peer
  multiples. Use after collecting data from compare_stocks_tool (for peers) and get_equity_snapshot_tool
  or run_equity_analysis_tool (for the target). Produces a 7-section relative valuation report.
tools-required:
  - mcp__agentman-alpha__compare_stocks_tool
  - mcp__agentman-alpha__get_equity_snapshot_tool
  - mcp__agentman-alpha__run_equity_analysis_tool (recommended)
estimated-time: 1-3 min
output-format: PDF or DOCX titled "Agentman — Comparable Company Valuation", authored by "Agentman Equity Research Assistant"
---

# Comparable Company Valuation

You are producing a relative valuation report using Comparable Company Analysis (Comps). You have collected data from:
1. **Equity Snapshot or Equity Analysis** (target stock) — P/E, P/B, P/S, EV/EBITDA, ROE, market cap, EPS, revenue, book value, debt
2. **Compare Stocks** (target + 3-5 peers) — side-by-side multiples, returns, volatility

Reference the **advanced-valuation-methodology** skill for formulas, weighting schemes, and interpretation guidelines.

## Data Extraction Checklist

### From Target Stock (Snapshot / Equity Analysis)
- [ ] Current price and market cap
- [ ] Shares outstanding (compute: market cap / price if not directly available)
- [ ] TTM EPS
- [ ] TTM Revenue
- [ ] Book value per share (compute: total equity / shares outstanding)
- [ ] TTM EBITDA (or approximate: operating income + D&A)
- [ ] Total debt and net debt (total debt - cash)
- [ ] Enterprise value (market cap + total debt - cash)
- [ ] P/E, P/S, P/B, EV/EBITDA (from data or computed)
- [ ] Revenue growth rate, operating margin, ROE

### From Peer Group (Compare Stocks)
- [ ] P/E for each peer
- [ ] P/B for each peer
- [ ] ROE for each peer
- [ ] 1Y return, volatility for each peer
- [ ] Compute: median, 25th percentile, 75th percentile for each multiple across peers
- [ ] Note: P/S and EV/EBITDA may need to be approximated from available data or flagged as unavailable

## Computation Steps

### Step 1: Validate Peer Group
- Confirm 3-5 peers in same or adjacent sub-industry
- Note any significant size/growth/margin mismatches
- If a peer has negative earnings, exclude it from P/E median calculation (not from other multiples)

### Step 2: Compute Peer Statistics
For each multiple (P/E, EV/EBITDA, P/S, P/B):
```
Median = middle value of peer set
P25 = 25th percentile (low bound)
P75 = 75th percentile (high bound)
Mean = arithmetic average (for reference, prefer median)
```

### Step 3: Determine Weights
Apply the default weighting from the advanced-valuation-methodology skill:
- P/E 35%, EV/EBITDA 30%, P/S 20%, P/B 15%
- Adjust if target has negative EPS or negative EBITDA (see skill for rules)
- Document the final weights used and why

### Step 4: Compute Implied Values
```
P/E implied  = Peer Median P/E x Target TTM EPS
P/S implied  = Peer Median P/S x (Target TTM Revenue / Shares Outstanding)
P/B implied  = Peer Median P/B x Target Book Value per Share
EV/EBITDA implied = (Peer Median EV/EBITDA x Target TTM EBITDA - Net Debt) / Shares Outstanding
```

### Step 5: Compute Weighted Fair Value
```
Fair Value = Sum(Weight_i x Implied Value_i)
Low Bound  = Sum(Weight_i x Implied Value using P25 multiples)
High Bound = Sum(Weight_i x Implied Value using P75 multiples)
```

### Step 6: Assess Premium/Discount
Compare target's growth, margins, market position, balance sheet, and analyst sentiment vs. peer medians. Determine if a premium (+5% to +20%) or discount (-5% to -15%) is warranted. Apply to the fair value range.

## Report Structure

### Header
```
# Agentman — Comparable Company Valuation: {Company Name} ({TICKER})

**Date**: {date} | **Price**: ${price} | **Market Cap**: ${market_cap}
**Peer Group**: {PEER1}, {PEER2}, {PEER3}[, {PEER4}, {PEER5}]
**Analyst**: Agentman Equity Research Assistant
```

### Section 1: Executive Summary (3-4 sentences)
- State the comps-implied fair value and range
- Note whether the stock appears overvalued, fairly valued, or undervalued vs. peers
- Highlight the most informative multiple and why
- Mention any premium/discount adjustment applied

### Section 2: Peer Group Selection
| Company | Ticker | Market Cap | Sector | Revenue Growth | Op. Margin |
|---------|--------|-----------|--------|----------------|------------|
| Target | ... | ... | ... | ... | ... |
| Peer 1 | ... | ... | ... | ... | ... |
| Peer 2 | ... | ... | ... | ... | ... |
| Peer 3 | ... | ... | ... | ... | ... |

Justify peer selection in 2-3 sentences. Note any compromises (e.g., "XYZ is 3x larger but the closest business model match").

### Section 3: Multiple Comparison
| Multiple | Target | Peer 1 | Peer 2 | Peer 3 | Median | P25 | P75 |
|----------|--------|--------|--------|--------|--------|-----|-----|
| P/E | ... | ... | ... | ... | ... | ... | ... |
| EV/EBITDA | ... | ... | ... | ... | ... | ... | ... |
| P/S | ... | ... | ... | ... | ... | ... | ... |
| P/B | ... | ... | ... | ... | ... | ... | ... |

Highlight where the target trades at a significant premium or discount to peer median. Bold the most notable deviation.

### Section 4: Implied Valuations
| Multiple | Weight | Peer Median | Implied Value | vs. Current Price |
|----------|--------|-------------|---------------|-------------------|
| P/E | {w}% | {val}x | ${implied} | {+/-pct}% |
| EV/EBITDA | {w}% | {val}x | ${implied} | {+/-pct}% |
| P/S | {w}% | {val}x | ${implied} | {+/-pct}% |
| P/B | {w}% | {val}x | ${implied} | {+/-pct}% |
| **Weighted Fair Value** | **100%** | — | **${fair_value}** | **{+/-pct}%** |

**Fair Value Range**: ${low_bound} (P25) to ${high_bound} (P75)

Explain the weighting rationale in 1-2 sentences. If weights were adjusted from defaults, state why.

### Section 5: Premium/Discount Assessment
| Factor | Target vs. Peers | Impact |
|--------|-----------------|--------|
| Revenue Growth | {faster/slower/in-line} | {+X% / -X% / neutral} |
| Profitability | {higher/lower margins} | {+X% / -X% / neutral} |
| Market Position | {leader/laggard} | {+X% / -X% / neutral} |
| Balance Sheet | {stronger/weaker} | {+X% / -X% / neutral} |
| Analyst Sentiment | {more/less bullish} | {+X% / -X% / neutral} |
| **Net Adjustment** | — | **{+/-X%}** |

**Adjusted Fair Value Range**: ${adj_low} to ${adj_high}

### Section 6: Investment Implications
- 2-3 paragraphs interpreting the results
- Compare comps-implied value to current price and (if available) DCF intrinsic value
- Discuss what would need to change for the stock to trade in line with peers
- Note the limitations: peer selection is subjective, multiples reflect market sentiment not intrinsic value

### Section 7: Key Risks & Caveats
- 3-5 bullets on methodology limitations and specific risks
- Always include: "Comps reflect relative value, not absolute intrinsic value — if the entire peer group is overvalued, the comps-implied value will also be elevated"
- Note data freshness and any approximations made

### Disclaimer
> *This Agentman comparable company analysis is for informational purposes only and does not constitute personalized investment advice. Peer selection and multiple weighting involve subjective judgment. Past performance does not guarantee future results. Investors should conduct their own due diligence and consult a licensed financial advisor. Prepared by Agentman Equity Research Assistant.*

## Formatting Rules
- Use `$` for all currency values, `B` for billions
- Round multiples to 1 decimal place (e.g., 25.3x)
- Round percentages to 1 decimal place
- Bold the weighted fair value and adjusted fair value range
- Use markdown tables for all structured data

## Brand Color Reference

All reports are output as **PDF or DOCX** (user's choice, PDF by default). Title: **"Agentman — Comparable Company Valuation"** (set in document metadata and cover page). Author: **Agentman Equity Research Assistant** (display in header/cover and footer). For DOCX, use `python-docx` with brand colors applied via `RGBColor`, table cell shading, and custom styles. Apply the Agentman brand palette from `references/brand-colors.md`, following the **agentman-pptx-style** design system.

- **Visual weight**: 70% Carbon/Charcoal, 20% Warm Neutrals, 10% Terracotta accent
- **Section titles**: `CHARCOAL_900` (#292322) with `AGENTMAN_500` (#CC785C) underline
- **Body text**: `CHARCOAL_950` (#141413); secondary `SLATE_600` (#475569)
- **Table headers**: `AGENTMAN_100` (#F6EAE6) light fill, `AGENTMAN_500` (#CC785C) terracotta text
- **Table borders**: `AGENTMAN_150` (#E3DACC) warm
- **Alternating table rows**: `AGENTMAN_50` (#FAF9F5) cream / white
- **Target trading at discount** (implied upside): `AGENTMAN_500` (#CC785C) terracotta bold
- **Target trading at premium** (implied downside): `AGENTMAN_600` (#A65945) deep terracotta bold
- **Premium/Discount Assessment** — positive: `AGENTMAN_500` terracotta; negative: `AGENTMAN_600` deep terracotta; neutral: `SLATE_600` (#475569)
- **Weighted Fair Value row**: `AGENTMAN_75` (#F0EEE6) warm cream highlight
- **Fair value range**: `AGENTMAN_700` (#8B4A38) accent for key values

**BANNED**: Green, red, amber, blue (except ✓/✗ comparison symbols). No gradients. No invented colors. See `references/color-antipatterns.md`.
