---
name: asset-based-valuation
description: |
  Perform an Asset-Based Valuation calculating the net asset value (NAV) per share from balance sheet
  data. Use after collecting data from run_equity_analysis_tool and get_equity_snapshot_tool to extract
  total assets, total liabilities, intangible assets, goodwill, and shares outstanding.
  Produces a 7-section asset-based valuation report.
tools-required:
  - mcp__agentman-alpha__run_equity_analysis_tool
  - mcp__agentman-alpha__get_equity_snapshot_tool
estimated-time: 1-2 min
output-format: PDF or DOCX titled "Agentman — Asset-Based Valuation", authored by "Agentman Equity Research Assistant"
---

# Asset-Based Valuation

You are producing a valuation report using the Asset-Based Approach, which values a company by computing the net worth of its assets minus liabilities. This method is particularly useful for asset-heavy firms, holding companies, financial institutions, and liquidation analysis. You have collected data from:
1. **Equity Analysis** — balance sheet data: total assets, total liabilities, tangible assets, intangible assets, goodwill, cash, property/plant/equipment, total equity
2. **Equity Snapshot** — current price, market cap, shares outstanding, key metrics (P/B ratio)

Reference the **advanced-valuation-methodology** skill for formulas, adjustment guidelines, and interpretation.

## Data Extraction Checklist

### From Equity Analysis (Balance Sheet — extract most recent + prior periods)
- [ ] Total assets
- [ ] Total liabilities
- [ ] Total stockholders' equity (book value)
- [ ] Cash and cash equivalents
- [ ] Short-term investments
- [ ] Net receivables
- [ ] Inventory
- [ ] Property, plant & equipment (net)
- [ ] Goodwill
- [ ] Intangible assets (other than goodwill)
- [ ] Long-term investments
- [ ] Total current assets
- [ ] Total current liabilities
- [ ] Long-term debt
- [ ] Short-term debt

### From Equity Snapshot
- [ ] Current stock price
- [ ] Market capitalization
- [ ] Shares outstanding (compute: market cap / price if not directly available)
- [ ] P/B ratio (Price-to-Book)
- [ ] Book value per share (if available, or compute: total equity / shares)

### Derived Metrics (compute these)
- [ ] Book Value per Share = Total Stockholders' Equity / Shares Outstanding
- [ ] Tangible Book Value = Total Equity - Goodwill - Intangible Assets
- [ ] Tangible Book Value per Share = Tangible Book Value / Shares Outstanding
- [ ] Net-Net Working Capital = (Current Assets - Total Liabilities) / Shares Outstanding
- [ ] Asset Composition (% tangible vs. intangible)
- [ ] Price-to-Tangible-Book = Current Price / Tangible Book Value per Share
- [ ] Price-to-Book = Current Price / Book Value per Share

## Computation Steps

### Step 1: Extract and Validate Balance Sheet Data

Gather the most recent balance sheet data (and prior year for trend analysis). Perform sanity checks:
- Total Assets should be positive
- Total Assets = Total Liabilities + Total Equity (verify accounting identity)
- Flag any large year-over-year changes (>25%) in goodwill or intangibles (may indicate acquisitions or impairments)

Present all extracted values in a table before computing.

### Step 2: Compute Book Value (Unadjusted NAV)

```
Book Value = Total Assets - Total Liabilities
Book Value per Share = Book Value / Shares Outstanding
```

This is the standard GAAP/IFRS book value. Note: this equals Total Stockholders' Equity on the balance sheet.

### Step 3: Compute Tangible Book Value (Adjusted NAV)

```
Tangible Book Value = Book Value - Goodwill - Other Intangible Assets
Tangible Book Value per Share = Tangible Book Value / Shares Outstanding
```

This strips out assets that may have zero realizable value in liquidation. This is the more conservative measure.

### Step 4: Compute Net-Net Working Capital (Graham's Method)

```
Net-Net Working Capital = Current Assets - Total Liabilities
NNWC per Share = Net-Net Working Capital / Shares Outstanding
```

Benjamin Graham's ultra-conservative floor valuation. A stock trading below NNWC per share is a deep value candidate (rare in modern markets).

### Step 5: Compute Adjusted Net Asset Value (if data permits)

Apply fair-value adjustments to key asset categories:

| Asset Category | Book Value | Adjustment Factor | Adjusted Value | Rationale |
|----------------|-----------|-------------------|----------------|-----------|
| Cash & equivalents | {val} | 1.00x | {val} | Face value |
| Short-term investments | {val} | 0.95-1.00x | {val} | Near face value |
| Net receivables | {val} | 0.85-0.95x | {val} | Discount for collectibility |
| Inventory | {val} | 0.50-0.80x | {val} | Liquidation discount |
| PP&E (net) | {val} | 0.60-1.20x | {val} | Market value vs. book |
| Goodwill | {val} | 0.00-0.50x | {val} | Often zero in liquidation |
| Other intangibles | {val} | 0.00-0.30x | {val} | IP/patents may retain some value |
| Long-term investments | {val} | 0.80-1.00x | {val} | Depends on liquidity |

```
Adjusted NAV = Sum of Adjusted Asset Values - Total Liabilities
Adjusted NAV per Share = Adjusted NAV / Shares Outstanding
```

**Adjustment factor guidelines** (from the advanced-valuation-methodology skill):
- Use higher factors for liquid, well-maintained assets
- Use lower factors for specialized, illiquid, or aging assets
- For asset-heavy industries (real estate, utilities, mining), PP&E may trade above book
- For tech/services companies, goodwill and intangibles are typically heavily discounted
- State your assumptions clearly

### Step 6: Compute Asset Composition

```
Tangible Asset Ratio = (Total Assets - Goodwill - Intangibles) / Total Assets
Intangible Asset Ratio = (Goodwill + Intangibles) / Total Assets
Current Asset Ratio = Current Assets / Total Assets
```

Categorize the company:
- **Asset-heavy** (Tangible > 70%): Real estate, utilities, mining, manufacturing — NAV is highly informative
- **Balanced** (Tangible 40-70%): Industrials, healthcare, financials — NAV is moderately informative
- **Asset-light** (Tangible < 40%): Tech, services, media — NAV is a floor, not a target

### Step 7: Historical Trend Analysis

Compare the current period to 2-3 prior periods:
```
Book Value Growth Rate = (Current BV - Prior BV) / Prior BV
```

Note trends in:
- Total equity growth (retained earnings accumulation)
- Goodwill growth (acquisition activity)
- PP&E growth (capital investment)
- Debt growth relative to asset growth

## Report Structure

### Header
```
# Agentman — Asset-Based Valuation: {Company Name} ({TICKER})

**Date**: {date} | **Price**: ${price} | **Market Cap**: ${market_cap}
**Methodology**: Net Asset Value (Book Value, Tangible Book Value, Adjusted NAV)
**Analyst**: Agentman Equity Research Assistant
```

### Section 1: Executive Summary (3-4 sentences)
- State the book value per share, tangible book value per share, and adjusted NAV per share
- Compare each to the current market price (premium/discount)
- Note the P/B and P/TBV ratios
- Identify whether the company is asset-heavy or asset-light and what that means for this methodology's relevance

### Section 2: Balance Sheet Overview
| Item | Current Period | Prior Period | Change |
|------|---------------|-------------|--------|
| Total Assets | ${val} | ${val} | {+/-pct}% |
| Total Liabilities | ${val} | ${val} | {+/-pct}% |
| Total Equity (Book Value) | ${val} | ${val} | {+/-pct}% |
| Goodwill | ${val} | ${val} | {+/-pct}% |
| Intangible Assets | ${val} | ${val} | {+/-pct}% |
| PP&E (net) | ${val} | ${val} | {+/-pct}% |
| Cash & Equivalents | ${val} | ${val} | {+/-pct}% |
| Current Assets | ${val} | ${val} | {+/-pct}% |
| Current Liabilities | ${val} | ${val} | {+/-pct}% |

Highlight any notable changes or red flags (e.g., goodwill doubling from an acquisition, declining PP&E from divestitures).

### Section 3: Asset-Based Valuation Summary
| Metric | Total Value | Per Share | vs. Market Price | Discount/Premium |
|--------|-----------|-----------|------------------|------------------|
| Book Value (GAAP) | ${val} | ${val} | ${price} | {+/-pct}% |
| Tangible Book Value | ${val} | ${val} | ${price} | {+/-pct}% |
| Net-Net Working Capital | ${val} | ${val} | ${price} | {+/-pct}% |
| Adjusted NAV | ${val} | ${val} | ${price} | {+/-pct}% |

**Key Ratios:**
| Ratio | Value | Interpretation |
|-------|-------|----------------|
| Price-to-Book (P/B) | {val}x | {Below 1.0 = trading below book, potential value} |
| Price-to-Tangible-Book (P/TBV) | {val}x | {Conservative floor measure} |
| Price / NNWC | {val}x | {Graham deep value if < 1.0} |
| Price / Adjusted NAV | {val}x | {Best estimate of asset-based fair value} |

### Section 4: Asset Composition Analysis
| Category | Value | % of Total Assets | Assessment |
|----------|-------|-------------------|------------|
| Cash & Short-Term Investments | ${val} | {pct}% | {Highly liquid} |
| Receivables | ${val} | {pct}% | {Near-term collectible} |
| Inventory | ${val} | {pct}% | {Liquidation value varies} |
| PP&E (net) | ${val} | {pct}% | {May be above/below book} |
| Goodwill | ${val} | {pct}% | {Zero in liquidation} |
| Other Intangibles | ${val} | {pct}% | {IP/patents: partial recovery} |
| Other Assets | ${val} | {pct}% | {Case-by-case} |

**Asset Profile**: {Asset-Heavy / Balanced / Asset-Light}

Tangible Asset Ratio: {pct}% — {interpretation of how informative NAV is for this company}

### Section 5: Adjusted NAV Detail
Show the adjustment table with your assumptions:

| Asset Category | Book Value | Adjustment | Adjusted Value | Rationale |
|----------------|-----------|------------|----------------|-----------|
| Cash & equivalents | ${val} | 1.00x | ${val} | Face value |
| Receivables | ${val} | {factor}x | ${val} | {rationale} |
| Inventory | ${val} | {factor}x | ${val} | {rationale} |
| PP&E | ${val} | {factor}x | ${val} | {rationale} |
| Goodwill | ${val} | {factor}x | ${val} | {rationale} |
| Intangibles | ${val} | {factor}x | ${val} | {rationale} |
| Other assets | ${val} | {factor}x | ${val} | {rationale} |
| **Total Adjusted Assets** | | | **${total}** | |
| Less: Total Liabilities | | | **(${liab})** | |
| **Adjusted NAV** | | | **${nav}** | |
| **Adjusted NAV per Share** | | | **${nav_ps}** | |

State your assumptions clearly and note which adjustments have the largest impact on the result.

### Section 6: Investment Implications
- 2-3 paragraphs interpreting the results in context
- Compare asset-based values to current price and (if available) DCF value, comps-implied value, and Merton value
- Discuss when the asset-based approach is most relevant for this particular company:
  - **Asset-heavy firms**: NAV is a primary valuation anchor
  - **Financial institutions**: Book value and tangible book value are key metrics
  - **Holding companies / conglomerates**: Sum-of-parts NAV is critical
  - **Distressed / liquidation scenarios**: Tangible book and NNWC matter most
  - **Asset-light / high-growth**: NAV provides a floor but earnings-based methods are primary
- Note the margin of safety (if any) provided by the asset base
- Discuss how the gap between market price and book value reflects the market's assessment of earnings power, intangible assets, and growth

### Section 7: Key Risks & Caveats
- 3-5 bullets on methodology limitations:
  - Book values reflect historical cost, not current market value (PP&E may be significantly over- or under-valued)
  - Goodwill and intangible asset adjustments are subjective
  - Does not capture earnings power, growth potential, or competitive advantages
  - Asset-light companies (tech, services) will have NAV far below market price by design
  - Balance sheet is a point-in-time snapshot; asset values can change rapidly
  - Off-balance-sheet items (operating leases, contingent liabilities) may not be fully reflected
- Always include: "Asset-based valuation is most informative for asset-heavy companies, financial institutions, and liquidation analysis. For companies where earnings power and growth drive value, DCF and Comps provide more relevant estimates."

### Disclaimer
> *This Agentman asset-based valuation report is for informational purposes only and does not constitute personalized investment advice. Book values and adjusted net asset values involve significant judgment in fair-value adjustments. Past performance does not guarantee future results. Investors should conduct their own due diligence and consult a licensed financial advisor. Prepared by Agentman Equity Research Assistant.*

## Formatting Rules
- Use `$` for all currency values, `B` for billions, `M` for millions
- Round per-share values to 2 decimal places
- Round percentages to 1 decimal place
- Round ratios to 2 decimal places
- Bold the final per-share values (book value, tangible book value, adjusted NAV)
- Use markdown tables for all structured data
- Present the base case values in bold in summary tables

## Brand Color Reference

All reports are output as **PDF or DOCX** (user's choice, PDF by default). Title: **"Agentman — Asset-Based Valuation"** (set in document metadata and cover page). Author: **Agentman Equity Research Assistant** (display in header/cover and footer). For DOCX, use `python-docx` with brand colors applied via `RGBColor`, table cell shading, and custom styles. Apply the Agentman brand palette from `references/brand-colors.md`, following the **agentman-pptx-style** design system.

- **Visual weight**: 70% Carbon/Charcoal, 20% Warm Neutrals, 10% Terracotta accent
- **Section titles**: `CHARCOAL_900` (#292322) with `AGENTMAN_500` (#CC785C) underline
- **Body text**: `CHARCOAL_950` (#141413); secondary `SLATE_600` (#475569)
- **Table headers**: `AGENTMAN_100` (#F6EAE6) light fill, `AGENTMAN_500` (#CC785C) terracotta text
- **Table borders**: `AGENTMAN_150` (#E3DACC) warm
- **Alternating table rows**: `AGENTMAN_50` (#FAF9F5) cream / white
- **Trading below book value** (potential value): `AGENTMAN_500` (#CC785C) terracotta bold
- **Trading at large premium to NAV**: `AGENTMAN_600` (#A65945) deep terracotta bold
- **Key NAV per-share values**: `AGENTMAN_700` (#8B4A38) accent
- **Adjustment factor column**: 1.0x (face value) = `AGENTMAN_500` terracotta; moderate discounts = `CHARCOAL_950` bold; heavy discounts = `AGENTMAN_600` deep terracotta
- **Asset profile**: "Asset-Heavy" (informative) = `AGENTMAN_500` terracotta; "Asset-Light" (floor only) = `AGENTMAN_400` (#D97757) highlight
- **Highlight rows** (totals, Adjusted NAV): `AGENTMAN_75` (#F0EEE6) warm cream

**BANNED**: Green, red, amber, blue (except ✓/✗ comparison symbols). No gradients. No invented colors. See `references/color-antipatterns.md`.
