---
name: dcf-valuation-analysis
description: |
  Interpret DCF valuation results from the Damodaran model with proper context, assumption analysis,
  and caveats. Use after collecting data from get_valuation_tool and optionally get_equity_snapshot_tool.
  Produces a valuation report with intrinsic value assessment and sensitivity discussion.
tools-required:
  - mcp__agentman-alpha__get_valuation_tool
  - mcp__agentman-alpha__get_equity_snapshot_tool (optional, for context)
estimated-time: 2-4 min
output-format: PDF or DOCX titled "Agentman — DCF Valuation Analysis", authored by "Agentman Equity Research Assistant"
---

# DCF Valuation Analysis

You are producing an intrinsic value assessment using Damodaran's DCF model output. The valuation tool returns an estimated value per share, the assumptions used, and the current market price.

## Data Extraction Checklist

### From DCF Valuation Tool
- [ ] Estimated intrinsic value per share
- [ ] Current market price
- [ ] Price as percentage of intrinsic value
- [ ] Valuation status (undervalued/overvalued/significantly_overvalued)
- [ ] Revenue growth rate (next year)
- [ ] 5-year revenue CAGR
- [ ] Operating margin (current)
- [ ] Target operating margin
- [ ] Years to converge
- [ ] Sales/capital ratio (years 1-5)
- [ ] Sales/capital ratio (years 6-10)
- [ ] Industry classification (US and global)
- [ ] Country (for risk-free rate)

### From Snapshot (if available)
- [ ] Current P/E, P/B, P/S
- [ ] Analyst price targets (avg, median, high, low)
- [ ] Analyst consensus rating
- [ ] Recent price performance

## Report Structure

### Header
```
# Agentman — DCF Valuation: {Company Name} ({TICKER})

**Model**: Damodaran Discounted Cash Flow | **Date**: {date}
**Analyst**: Agentman Equity Research Assistant
```

### Section 1: Valuation Result
Key findings table:
| | |
|---|---|
| **Estimated Intrinsic Value** | **${value} / share** |
| **Current Market Price** | **${price} / share** |
| **Price as % of Intrinsic Value** | **{pct}%** |
| **Valuation Status** | **{status}** |

Follow with a 1-2 sentence headline interpretation (e.g., "The DCF model estimates {TICKER} trades at roughly {X}x its intrinsic value").

### Section 2: Key Assumptions Used
| Parameter | Value | Notes |
|-----------|-------|-------|
| Revenue Growth (Next Year) | {pct}% | Compare to analyst consensus if available |
| 5-Year Revenue CAGR | {pct}% | Note if conservative/aggressive vs. historical |
| Operating Margin (Current) | {pct}% | Compare to actual TTM margin |
| Target Operating Margin | {pct}% | Note direction of margin change |
| Years to Converge | ~{years} | ... |
| Sales/Capital Ratio (Yr 1-5) | {ratio} | Higher = more capital-efficient |
| Sales/Capital Ratio (Yr 6-10) | {ratio} | ... |
| Industry Classification | {industry} | Flag if misclassified |
| Country (Risk-Free Rate) | {country} | ... |

### Section 3: Interpreting the Results

Structure into three subsections:

#### What the model captures well
2-3 bullets explaining which assumptions are reasonable and well-calibrated. Reference specific numbers.

#### What the model may undervalue
3-4 bullets covering factors the DCF doesn't capture:
- Growth optionality (new products, markets, AI)
- Ecosystem/moat value (switching costs, network effects)
- Capital return programs (buybacks, dividends)
- Brand/intangible value
- Segment-level growth differences (blended CAGR masks faster-growing segments)

#### What could justify the premium
If overvalued: explain what growth rate, margin, or multiple the market is implicitly assuming to justify the current price. Frame as: "To close the gap between ${dcf_value} and ${current_price}, the market is implicitly assuming..."

If undervalued: explain what risks or concerns may be creating the discount.

### Section 4: Context (if snapshot data available)
Compare the DCF result to other valuation anchors:
- DCF value vs. analyst median price target
- DCF value vs. current P/E relative to sector
- DCF value vs. historical valuation range
- How the valuation status relates to recent price performance

### Section 5: Cross-Stock DCF Comparison (if comparing multiple)
If the user has previously run DCF on other tickers in the conversation, include:
| Metric | TICK1 | TICK2 | TICK3 |
|--------|-------|-------|-------|
| Intrinsic Value | ... | ... | ... |
| Current Price | ... | ... | ... |
| Price / Intrinsic Value | ... | ... | ... |
| 5-Year CAGR Assumed | ... | ... | ... |
| Target Op. Margin | ... | ... | ... |

Ranking by valuation attractiveness with rationale.

### Section 7: Investor Profile Implications

Using the DCF result and available metrics, assess how the valuation finding affects each investor profile:

| Profile | DCF Tolerance | Current Price/DCF | Assessment |
|---------|--------------|-------------------|------------|
| **Conservative** | <= 1.1x (margin of safety required) | {ratio}x | {Attractive / Borderline / Too expensive} |
| **Moderate** | Up to ~1.5x | {ratio}x | {Attractive / Acceptable / Stretched} |
| **Aggressive** | 2-3x+ for high growth | {ratio}x | {Deep value / Reasonable / Fully priced} |

Brief interpretation (2-3 sentences):
- For **conservative investors**: State whether the DCF provides a margin of safety. If the stock trades above 1.1x intrinsic value, note it fails the conservative valuation threshold and what price would be needed.
- For **moderate investors**: Assess whether the growth rate justifies the premium. Reference PEG or analyst consensus if available.
- For **aggressive investors**: Focus on whether the growth assumptions in the DCF are conservative relative to the company's trajectory, and what upside exists if growth exceeds assumptions.

### Section 8: Bottom Line
2-3 sentence synthesis. Frame as: "The DCF model {flags/suggests}... However, {context/caveats}... For investors who {belief about growth/moat}, {implication}."

### Disclaimer
> *This Agentman valuation report is for informational purposes only and does not constitute personalized investment advice. DCF models are highly sensitive to input assumptions — small changes in growth rates or discount rates can materially alter the output. Investors should conduct their own due diligence and consult a licensed financial advisor. Prepared by Agentman Equity Research Assistant.*

## Critical Interpretation Guidelines

1. **Never present the DCF value as "the right price."** Frame it as one data point among many.
2. **Always flag if the industry classification seems wrong** (e.g., Apple classified as "Computer Software" when it's primarily hardware + services).
3. **If the revenue growth assumption is negative or near-zero for a growing company**, explicitly note this as conservative and explain the impact.
4. **Compare the model's CAGR to consensus estimates** — if the model uses 5% and analysts expect 15%, that explains much of the "overvaluation."
5. **Buyback-heavy companies** will appear more overvalued on DCF because the model doesn't fully credit share count reduction.
6. **The model is most reliable** for mature, predictable-cash-flow businesses and least reliable for high-growth, pre-profit companies.

## Brand Color Reference

All reports are output as **PDF or DOCX** (user's choice, PDF by default). Title: **"Agentman — DCF Valuation Analysis"** (set in document metadata and cover page). Author: **Agentman Equity Research Assistant** (display in header/cover and footer). For DOCX, use `python-docx` with brand colors applied via `RGBColor`, table cell shading, and custom styles. Apply the Agentman brand palette from `references/brand-colors.md`, following the **agentman-pptx-style** design system.

- **Visual weight**: 70% Carbon/Charcoal, 20% Warm Neutrals, 10% Terracotta accent
- **Section titles**: `CHARCOAL_900` (#292322) with `AGENTMAN_500` (#CC785C) underline
- **Body text**: `CHARCOAL_950` (#141413); secondary `SLATE_600` (#475569)
- **Table headers**: `AGENTMAN_100` (#F6EAE6) light fill, `AGENTMAN_500` (#CC785C) terracotta text
- **Table borders**: `AGENTMAN_150` (#E3DACC) warm
- **Alternating table rows**: `AGENTMAN_50` (#FAF9F5) cream / white
- **Valuation status "Undervalued"**: `AGENTMAN_500` (#CC785C) terracotta bold
- **Valuation status "Overvalued"**: `AGENTMAN_600` (#A65945) deep terracotta bold
- **Valuation status "Fairly Valued"**: `CHARCOAL_950` (#141413) bold
- **Verdict box**: `AGENTMAN_500` (#CC785C) border + `AGENTMAN_50` (#FAF9F5) cream bg (all verdicts use same box style)
- **Sensitivity table base case**: `AGENTMAN_75` (#F0EEE6) highlight row
- **DCF intrinsic value**: `AGENTMAN_700` (#8B4A38) accent for key metric
- **Terracotta budget**: max 3 `AGENTMAN_500` elements per section

**BANNED**: Green, red, amber, blue (except ✓/✗ comparison symbols). No gradients. No invented colors. See `references/color-antipatterns.md`.
