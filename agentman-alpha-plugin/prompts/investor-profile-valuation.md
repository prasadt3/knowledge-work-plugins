---
name: investor-profile-valuation
description: |
  Score and evaluate a stock across Conservative, Moderate, and Aggressive investor profiles using a
  50-point rubric per profile. Use after collecting data from get_equity_snapshot_tool, run_equity_analysis_tool,
  and get_valuation_tool. Produces a profile scoring report with best-fit determination and action guidance.
tools-required:
  - mcp__agentman-alpha__get_equity_snapshot_tool
  - mcp__agentman-alpha__run_equity_analysis_tool
  - mcp__agentman-alpha__get_valuation_tool
estimated-time: 3-5 min
output-format: PDF or DOCX titled "Agentman — Investor Profile Valuation", authored by "Agentman Equity Research Assistant"
---

# Investor Profile Valuation

You are producing a profile-based stock evaluation that scores a stock across three investor risk profiles (Conservative, Moderate, Aggressive) using the investor-profile-methodology skill's scoring rubric.

## Data Extraction Checklist

Before scoring, extract these values from tool output:

### From Equity Snapshot / Equity Analysis
- [ ] Current price, 52-week range, % from 52-week high
- [ ] P/E (TTM), P/B, P/S, EV/EBITDA
- [ ] ROE, gross margin, operating margin, net margin
- [ ] Beta, annualized volatility
- [ ] Dividend yield
- [ ] Revenue (last 2-4 years) and YoY growth rates
- [ ] EPS (last 2-4 years) and trend direction
- [ ] Debt-to-equity, current ratio
- [ ] Free cash flow trend
- [ ] Analyst consensus rating, buy/hold/sell counts
- [ ] Analyst price targets (high, median, average, low)
- [ ] 1M, 3M, 6M, 1Y returns
- [ ] 50-day and 200-day moving averages

### From DCF Valuation
- [ ] Estimated intrinsic value per share
- [ ] Price as multiple of intrinsic value (price / DCF value)
- [ ] Revenue growth rate assumption
- [ ] 5-year CAGR assumption
- [ ] Target operating margin
- [ ] Industry classification

### Derived Metrics (compute these)
- [ ] PEG ratio (P/E / EPS growth rate)
- [ ] Implied analyst upside (median PT vs price)
- [ ] Analyst high target upside (high PT vs price)
- [ ] Buy rating percentage (buy + strong buy / total ratings)
- [ ] Max drawdown approximation (% from 52-week high)
- [ ] Price vs 50-day MA (% above/below)

## Scoring Computation

For each profile, score every criterion using the thresholds from the investor-profile-methodology skill. Record both sub-component scores and the criterion total.

### Scoring Process
1. Look up the data value for each sub-component
2. Match it to the threshold table for the appropriate profile
3. Assign the point value (1-5)
4. Sum both sub-components for the criterion total (max 10)
5. Sum all 5 criteria for the profile total (max 50)
6. If a data point is unavailable, note "N/A" and score conservatively (2 pts)

## Report Structure

### Header — CRITICAL: Agentman Branding Required

The first line of every report MUST begin with "Agentman —". This is the product brand and must ALWAYS appear as the title prefix. The analyst line MUST read "Equity Research Assistant". Never omit either element.

```
# Agentman — Investor Profile Analysis: {Company Name} ({TICKER})

**Date**: {date} | **Price**: ${price} | **Sector**: {sector}
**Analyst**: Equity Research Assistant
```

When generating the PDF/DOCX, the page 1 title MUST render as:
- **Title line**: "Agentman — Investor Profile Analysis: {Company Name} ({TICKER})"
- **Subtitle/analyst line**: "Equity Research Assistant | {date}"
- Set document metadata title to "Agentman — Investor Profile Analysis: {Company Name} ({TICKER})"
- Set document metadata author to "Agentman Equity Research Assistant"

Do NOT omit "Agentman —" from the title. Do NOT use only the company name as the title.

### Section 1: Profile Scores Summary

| Profile | Score | Rating | Key Strength | Key Gap |
|---------|-------|--------|-------------|---------|
| Conservative | {X}/50 | {rating} | {best criterion} | {worst criterion} |
| Moderate | {X}/50 | {rating} | {best criterion} | {worst criterion} |
| Aggressive | {X}/50 | {rating} | {best criterion} | {worst criterion} |

**Best Fit**: {profile} ({score}/50 — {rating})

### Section 2: Conservative Profile Detail

#### Score Breakdown
| # | Criterion | Sub-1 | Sub-2 | Total | Notes |
|---|-----------|-------|-------|-------|-------|
| 1 | Dividend Yield & Consistency | {pts}/5 | {pts}/5 | {pts}/10 | {key data point} |
| 2 | Balance Sheet Strength | {pts}/5 | {pts}/5 | {pts}/10 | {key data point} |
| 3 | Earnings Stability | {pts}/5 | {pts}/5 | {pts}/10 | {key data point} |
| 4 | Valuation Margin of Safety | {pts}/5 | {pts}/5 | {pts}/10 | {key data point} |
| 5 | Low Volatility / Beta | {pts}/5 | {pts}/5 | {pts}/10 | {key data point} |
| | **Total** | | | **{X}/50** | **{rating}** |

#### Conservative Assessment
2-3 sentences: Is this stock suitable for conservative investors? What's the primary appeal or concern? Reference specific data.

#### Conservative Action Guidance
- **Position sizing**: {recommendation based on score}
- **Entry strategy**: {margin of safety / yield requirement}
- **Key risk to monitor**: {primary conservative risk factor}

### Section 3: Moderate Profile Detail

#### Score Breakdown
| # | Criterion | Sub-1 | Sub-2 | Total | Notes |
|---|-----------|-------|-------|-------|-------|
| 1 | Growth-Value Balance / PEG | {pts}/5 | {pts}/5 | {pts}/10 | {key data point} |
| 2 | Profitability Quality | {pts}/5 | {pts}/5 | {pts}/10 | {key data point} |
| 3 | Analyst Consensus Strength | {pts}/5 | {pts}/5 | {pts}/10 | {key data point} |
| 4 | Reasonable Valuation | {pts}/5 | {pts}/5 | {pts}/10 | {key data point} |
| 5 | Risk-Adjusted Return Potential | {pts}/5 | {pts}/5 | {pts}/10 | {key data point} |
| | **Total** | | | **{X}/50** | **{rating}** |

#### Moderate Assessment
2-3 sentences: Does this stock offer the right growth-value balance? Reference PEG, analyst consensus, and risk-adjusted return.

#### Moderate Action Guidance
- **Position sizing**: {recommendation}
- **Entry strategy**: {valuation anchor or catalyst timing}
- **Key metric to watch**: {most important metric for this profile}

### Section 4: Aggressive Profile Detail

#### Score Breakdown
| # | Criterion | Sub-1 | Sub-2 | Total | Notes |
|---|-----------|-------|-------|-------|-------|
| 1 | Revenue Growth Rate | {pts}/5 | {pts}/5 | {pts}/10 | {key data point} |
| 2 | Market Position & TAM | {pts}/5 | {pts}/5 | {pts}/10 | {key data point} |
| 3 | Momentum & Technical Strength | {pts}/5 | {pts}/5 | {pts}/10 | {key data point} |
| 4 | Innovation / Disruption Potential | {pts}/5 | {pts}/5 | {pts}/10 | {key data point} |
| 5 | Upside to Price Targets | {pts}/5 | {pts}/5 | {pts}/10 | {key data point} |
| | **Total** | | | **{X}/50** | **{rating}** |

#### Aggressive Assessment
2-3 sentences: Does this stock have the growth velocity and catalyst density for aggressive portfolios? Reference revenue growth, momentum, and upside.

#### Aggressive Action Guidance
- **Position sizing**: {recommendation}
- **Entry strategy**: {momentum trigger or catalyst timing}
- **Key catalyst**: {upcoming event or inflection point}

### Section 5: Best Fit Determination

Identify the profile with the highest score. If scores are close (within 5 points), discuss the nuance.

**Recommended Profile**: {profile}

1-2 paragraph narrative explaining:
- Why this profile is the best fit, with data citations
- What the stock offers to this investor type
- Any caveats or conditions on the recommendation

### Section 6: Cross-Profile Action Summary

| Investor Type | Verdict | Position Size | Entry Point | Time Horizon |
|---------------|---------|---------------|-------------|--------------|
| Conservative | {Buy/Hold/Avoid} | {range}% | {condition} | {horizon} |
| Moderate | {Buy/Hold/Avoid} | {range}% | {condition} | {horizon} |
| Aggressive | {Buy/Hold/Avoid} | {range}% | {condition} | {horizon} |

### Disclaimer
> *This Agentman investor profile analysis is for informational purposes only and does not constitute personalized investment advice. Profile scores are based on quantitative screening criteria and do not account for individual financial situations, tax considerations, or complete portfolio context. Investors should conduct their own due diligence and consult a licensed financial advisor. Prepared by Agentman Equity Research Assistant.*

## Formatting Rules
- Show all scores as "{X}/Y" format for clarity
- Bold the highest-scoring profile in the summary table
- Use the rating labels from the interpretation guide (Excellent Fit, Good Fit, etc.)
- Round all percentages to 1 decimal place
- If a criterion cannot be scored due to missing data, explain why and assign 2 pts default

## Brand Color Reference

All reports are output as **PDF or DOCX** (user's choice, PDF by default). Title: **"Agentman — Investor Profile Valuation"** (set in document metadata and cover page). Author: **Agentman Equity Research Assistant** (display in header/cover and footer). For DOCX, use `python-docx` with brand colors applied via `RGBColor`, table cell shading, and custom styles. Apply the Agentman brand palette from `references/brand-colors.md`, following the **agentman-pptx-style** design system. Quiet confidence — charcoal suits, not fire trucks.

- **Visual weight**: 70% Carbon/Charcoal, 20% Warm Neutrals, 10% Terracotta accent
- **Section titles**: `CHARCOAL_900` (#292322) with `AGENTMAN_500` (#CC785C) underline
- **Body text**: `CHARCOAL_950` (#141413); secondary `SLATE_600` (#475569)
- **Table headers**: `AGENTMAN_100` (#F6EAE6) light fill, `AGENTMAN_500` (#CC785C) terracotta text
- **Table borders**: `AGENTMAN_150` (#E3DACC) warm
- **Alternating rows**: `AGENTMAN_50` (#FAF9F5) cream / white
- **Best Fit row**: `AGENTMAN_75` (#F0EEE6) warm cream highlight
- **Score badges**: All badges `AGENTMAN_100` bg + `AGENTMAN_800` text + `AGENTMAN_200` border. No color-coded tiers — differentiation via text wording only.
- **Score bars**: `AGENTMAN_150` (#E3DACC) track + `AGENTMAN_500` (#CC785C) fill — same for ALL tiers
- **Sub-score emphasis**: High (4-5 pts) = `AGENTMAN_500` terracotta bold; Mid (2-3 pts) = `CHARCOAL_950` bold; Low (1 pt) = `AGENTMAN_600` (#A65945) deep terracotta
- **Verdict text**: "Buy" = `AGENTMAN_500` terracotta bold; "Hold" = `CHARCOAL_950` bold; "Avoid" = `AGENTMAN_600` deep terracotta bold
- **Callout/highlight boxes**: `AGENTMAN_75` cream bg or `AGENTMAN_500` border + `AGENTMAN_50` cream bg. Heading: `CHARCOAL_900`, never colored.
- **Terracotta budget**: max 3 `AGENTMAN_500` elements per section

**BANNED**: Green, red, amber, blue (except ✓/✗ comparison symbols). No gradients. No invented colors. See `references/color-antipatterns.md`.
