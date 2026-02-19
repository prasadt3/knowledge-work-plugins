---
name: financial-data-specialist
description: |
  Use when interpreting financial data, analyzing portfolios, tracking earnings, or presenting securities metrics. Provides frameworks for turning raw market data into clear, actionable insights.
---

This skill provides frameworks for interpreting and presenting financial data from equity analysis tools.

## Securities Data Analysis

### Key Financial Metrics Interpretation

| Category | Metrics | Context |
|----------|---------|---------|
| **Valuation** | P/E (TTM & Forward), P/B, P/S, EV/EBITDA, PEG | Compare to sector averages; P/E < 15 cheap, > 30 expensive (varies by sector) |
| **Profitability** | Gross Margin, Operating Margin, Net Margin, ROE, ROA | ROE > 15% strong, > 25% exceptional; compare to peers |
| **Growth** | Revenue Growth (YoY), EPS Growth, FCF Growth | > 20% YoY is high growth; declining rates signal maturation |
| **Dividends** | Yield, Payout Ratio, Growth Rate | Payout > 80% may be unsustainable; track growth consistency |
| **Balance Sheet** | Debt/Equity, Current Ratio, Quick Ratio | D/E > 2 is leveraged; Current Ratio > 1.5 is healthy |

### Data Quality Checks
- Note data timestamps and freshness
- Flag when data may be delayed vs. real-time
- Identify missing or zero values that may indicate data issues
- Cross-reference metrics when possible (e.g., P/E from different sources)

## Earnings Analysis Framework

### Earnings Results Assessment
- **Beat/Miss Magnitude**: Compare to historical beat/miss patterns
- **Revenue Quality**: Organic vs. acquisition-driven growth
- **Margin Trends**: Expanding margins are positive; flag compression
- **Guidance**: Above/below consensus signals management confidence
- **Revisions**: Post-earnings estimate revisions indicate market reaction

### Earnings Context
- Compare to same quarter prior year (seasonality)
- Track sequential improvement/deterioration
- Assess guidance credibility based on historical accuracy

## Portfolio Analysis Framework

### Portfolio Snapshot Template
| Ticker | Current Price | Day Change | P/E | ROE | Dividend Yield | Analyst Rating |
|--------|--------------|------------|-----|-----|----------------|----------------|

### Performance Attribution
- Calculate weighted returns by position size
- Identify best/worst contributors
- Compare to relevant benchmark (S&P 500, sector ETF)

### Risk Assessment
- **Concentration**: Flag if any holding > 20% of portfolio
- **Sector Exposure**: Identify over/under-weight sectors
- **Correlation**: Note highly correlated holdings that increase risk
- **Dividend Dependence**: Flag if income relies on few positions

## Presentation Best Practices

### Securities Data Report
1. **Price Summary**: Current quote with key stats in a compact format
2. **Valuation Metrics**: Table of key ratios with sector context
3. **Financial Highlights**: Recent performance vs. prior periods
4. **Upcoming Events**: Earnings dates, ex-dividend dates
5. **One-Sentence Assessment**: Quick take on valuation

### Portfolio Report
1. **Executive Summary**: Total value, performance vs. benchmark, yield
2. **Holdings Table**: Position details with key metrics
3. **Allocation Overview**: Sector breakdown, concentration analysis
4. **Action Items**: Specific rebalancing or optimization suggestions

## Brand Color & Styling

All output MUST use the Agentman brand palette from `references/brand-colors.md`, following the **agentman-pptx-style** design system. Quiet confidence — charcoal suits, not fire trucks.

- **Visual weight**: 70% Carbon/Charcoal, 20% Warm Neutrals, 10% Terracotta accent. Max 3 `AGENTMAN_500` elements per section.
- **Table headers**: `AGENTMAN_100` (#F6EAE6) light fill + `AGENTMAN_500` (#CC785C) terracotta text
- **Table borders**: `AGENTMAN_150` (#E3DACC) warm borders
- **Body text**: `CHARCOAL_950` (#141413); section titles in `CHARCOAL_900` (#292322) with `AGENTMAN_500` (#CC785C) underline
- **Alternating table rows**: `AGENTMAN_50` (#FAF9F5) cream / white; highlight rows in `AGENTMAN_75` (#F0EEE6)
- **Emphasis text**: `AGENTMAN_500` (#CC785C) positive, `AGENTMAN_600` (#A65945) negative, `AGENTMAN_400` (#D97757) caution, `CHARCOAL_950` neutral bold
- **BANNED**: Green, red, amber, blue (except ✓/✗ symbols). No gradients. No invented colors.
