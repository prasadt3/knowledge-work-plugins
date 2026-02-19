---
name: market-analyst-pro
description: |
  Use when analyzing sectors, comparing multiple stocks, identifying market trends, or assessing competitive positioning. Provides structured frameworks for sector analysis, comparative rankings, and trend identification.
---

This skill provides frameworks for market analysis, sector intelligence, and multi-security comparisons.

## Sector Analysis Framework

### Sector Performance Assessment
- **Absolute Performance**: Total return over multiple timeframes (1M, 3M, YTD, 1Y)
- **Relative Performance**: vs. S&P 500 to identify outperformance/underperformance
- **Rotation Positioning**: Where the sector sits in the economic cycle (early/mid/late)
- **Earnings Trends**: Growth rates and revision direction

### Sector-Specific Factors

| Sector | Key Drivers to Analyze |
|--------|----------------------|
| Technology | Innovation cycles, capex trends, cloud/AI adoption, regulatory risk |
| Healthcare | Drug pipelines, regulatory environment, demographic tailwinds |
| Financials | Net interest margins, credit quality, capital markets activity |
| Energy | Supply/demand dynamics, OPEC policy, energy transition progress |
| Consumer | Spending trends, inventory levels, pricing power, sentiment |
| Industrials | Capex cycles, infrastructure spending, supply chain health |

## Comparative Analysis Framework

### Comparison Matrix Template
| Metric | Stock A | Stock B | Stock C | Sector Avg |
|--------|---------|---------|---------|------------|
| P/E (TTM) | | | | |
| Forward P/E | | | | |
| P/B | | | | |
| ROE | | | | |
| Revenue Growth | | | | |
| 1Y Return | | | | |
| Volatility | | | | |
| Analyst Rating | | | | |

### Ranking Methodology
For each comparison, rank stocks across dimensions:
1. **Value**: Lowest P/E and P/B relative to growth (PEG)
2. **Growth**: Highest revenue and earnings growth rates
3. **Quality**: Highest ROE, margins, and balance sheet strength
4. **Momentum**: Best recent returns (1M, 3M, 1Y)
5. **Risk**: Lowest volatility and beta
6. **Sentiment**: Strongest analyst consensus and price target upside

### Relative Value Assessment
- Compare PEG ratios to identify undervalued-relative-to-growth stocks
- Assess price target upside/downside for each
- Identify which stock offers the best risk-adjusted return potential

## Trend Identification

### Technical Trends
- Sector relative strength rankings (rotating leadership)
- Breakout/breakdown patterns in sector ETFs
- Volume and momentum divergences

### Fundamental Trends
- Earnings revision direction by sector
- Margin expansion vs. contraction themes
- Capital allocation shifts (buybacks vs. capex vs. M&A)

### Thematic Trends
- Secular growth themes: AI, electrification, demographics, reshoring
- Cyclical rotation signals: value vs. growth, large vs. small cap
- Factor performance trends

## Output Best Practices

### Summary Report
1. **Market Snapshot**: 3-4 bullet points on current conditions
2. **Sector Rankings**: Top/bottom performers with drivers
3. **Key Trends**: 2-3 actionable themes
4. **Watch List**: Stocks/sectors to monitor

### Comparison Report
1. **Comparison Matrix**: All metrics side-by-side, **bold the best** in each row
2. **Relative Value**: Which stock offers best value for money
3. **Growth Profile**: Sustainability of growth rates
4. **Risk-Adjusted Ranking**: Returns per unit of risk
5. **Final Recommendation**: Clear ranking with rationale

## Brand Color & Styling

All output MUST use the Agentman brand palette from `references/brand-colors.md`, following the **agentman-pptx-style** design system. Quiet confidence — charcoal suits, not fire trucks.

- **Visual weight**: 70% Carbon/Charcoal, 20% Warm Neutrals, 10% Terracotta accent. Max 3 `AGENTMAN_500` elements per section.
- **Table headers**: `AGENTMAN_100` (#F6EAE6) light fill + `AGENTMAN_500` (#CC785C) terracotta text
- **Table borders**: `AGENTMAN_150` (#E3DACC) warm borders
- **Body text**: `CHARCOAL_950` (#141413); section titles in `CHARCOAL_900` (#292322) with `AGENTMAN_500` (#CC785C) underline
- **Alternating table rows**: `AGENTMAN_50` (#FAF9F5) cream / white; sector average rows in `AGENTMAN_75` (#F0EEE6)
- **Best-in-class / leader**: `AGENTMAN_500` (#CC785C) terracotta bold
- **Worst-in-class / laggard**: `AGENTMAN_600` (#A65945) deep terracotta bold
- **Emphasis text**: `AGENTMAN_500` positive, `AGENTMAN_600` negative, `AGENTMAN_400` (#D97757) caution, `CHARCOAL_950` neutral bold
- **BANNED**: Green, red, amber, blue (except ✓/✗ symbols). No gradients. No invented colors.
