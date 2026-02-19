---
name: stock-analysis-specialist
description: |
  Use when analyzing individual stocks, performing DCF valuations, assessing risk profiles, or building investment theses. Provides fundamental, technical, and sentiment analysis frameworks for thorough stock evaluation.
---

This skill provides frameworks for holistic stock analysis combining fundamental, technical, and sentiment perspectives.

## Fundamental Analysis Framework

### Valuation Ratios Interpretation
| Ratio | Cheap | Fair | Expensive | Notes |
|-------|-------|------|-----------|-------|
| P/E (TTM) | < 15 | 15-25 | > 30 | Sector-dependent; tech typically higher |
| P/B | < 1 | 1-3 | > 5 | < 1 may signal distress or undervaluation |
| PEG | < 1 | 1-1.5 | > 2 | Best growth-adjusted valuation metric |
| EV/EBITDA | < 8 | 8-15 | > 20 | Useful for comparing leveraged companies |

### Profitability Assessment
| Metric | Weak | Average | Strong | Exceptional |
|--------|------|---------|--------|-------------|
| ROE | < 8% | 8-15% | 15-25% | > 25% |
| Net Margin | < 5% | 5-15% | 15-25% | > 25% |
| Gross Margin | < 30% | 30-50% | 50-70% | > 70% |

### Financial Health Checklist
- Debt-to-Equity < 1.5 (healthy), > 2 (leveraged)
- Current Ratio > 1.5 (adequate liquidity)
- Interest Coverage > 5x (comfortable debt service)
- Free Cash Flow positive and growing

## Technical Analysis Reference

### Key Indicators
| Indicator | Bullish Signal | Bearish Signal |
|-----------|---------------|----------------|
| RSI | < 30 (oversold) | > 70 (overbought) |
| MACD | Signal line crossover up | Signal line crossover down |
| 50/200 MA | Golden cross (50 > 200) | Death cross (50 < 200) |
| Volume | Increasing on up moves | Increasing on down moves |

### Support/Resistance Analysis
- Identify key price levels from historical peaks/troughs
- Note distance from 52-week high/low
- Assess trend direction (higher highs/lows vs. lower highs/lows)

## Sentiment Analysis Reference

### Analyst Ratings Interpretation
| Consensus | Interpretation | Signal |
|-----------|---------------|--------|
| Strong Buy (< 1.5) | Very bullish | Positive if recent upgrades |
| Buy (1.5-2.5) | Moderately bullish | Consensus positive |
| Hold (2.5-3.5) | Neutral | Watch for direction change |
| Sell (> 3.5) | Bearish | Caution warranted |

### Price Target Analysis
- **Upside > 20%**: Significant appreciation expected
- **Upside 10-20%**: Moderate upside
- **Upside < 10%**: Limited upside from current levels
- **Target Dispersion**: Wide range = high uncertainty

## Risk Assessment Framework

### Quantitative Risk
| Metric | Low Risk | Medium Risk | High Risk |
|--------|----------|-------------|-----------|
| Beta | < 0.8 | 0.8-1.2 | > 1.5 |
| Volatility (annualized) | < 20% | 20-35% | > 40% |
| Max Drawdown (1Y) | < 15% | 15-30% | > 30% |

### Qualitative Risk Factors
- **Company**: Execution risk, key person dependency, customer concentration
- **Industry**: Competitive disruption, regulatory changes, cyclicality
- **Macro**: Interest rate sensitivity, currency exposure, geopolitical risk

## DCF Valuation Context

When presenting Damodaran DCF results:
- Compare intrinsic value to current price for margin of safety
- Note key assumptions (revenue growth, operating margin, WACC)
- Emphasize that DCF is highly sensitive to inputs
- Cross-reference with P/E-based and analyst target-based valuations
- Present a range (bull/base/bear) rather than a single point estimate

## Investment Thesis Template
1. **Thesis Statement**: One sentence on why this stock is attractive/unattractive
2. **Key Drivers**: 3 factors that support the thesis
3. **Bull Case**: Best-case scenario with price target
4. **Bear Case**: Worst-case scenario with downside risk
5. **Catalysts**: Upcoming events that could move the stock
6. **Risk/Reward**: Summary of upside vs. downside probability

## Brand Color & Styling

All output MUST use the Agentman brand palette from `references/brand-colors.md`, following the **agentman-pptx-style** design system. Quiet confidence — charcoal suits, not fire trucks.

- **Visual weight**: 70% Carbon/Charcoal, 20% Warm Neutrals, 10% Terracotta accent. Max 3 `AGENTMAN_500` elements per section.
- **Table headers**: `AGENTMAN_100` (#F6EAE6) light fill + `AGENTMAN_500` (#CC785C) terracotta text
- **Table borders**: `AGENTMAN_150` (#E3DACC) warm borders
- **Body text**: `CHARCOAL_950` (#141413); section titles in `CHARCOAL_900` (#292322) with `AGENTMAN_500` (#CC785C) underline
- **Alternating table rows**: `AGENTMAN_50` (#FAF9F5) cream / white; highlight rows in `AGENTMAN_75` (#F0EEE6)
- **Bullish / undervalued / low risk**: `AGENTMAN_500` (#CC785C) terracotta bold
- **Bearish / overvalued / high risk**: `AGENTMAN_600` (#A65945) deep terracotta bold
- **Neutral / fair value / medium risk**: `CHARCOAL_950` (#141413) bold
- **Verdict boxes**: `AGENTMAN_500` (#CC785C) border + `AGENTMAN_50` (#FAF9F5) cream bg — same style for all verdicts
- **Key valuation metrics**: `AGENTMAN_700` (#8B4A38) accent
- **BANNED**: Green, red, amber, blue (except ✓/✗ symbols). No gradients. No invented colors.
