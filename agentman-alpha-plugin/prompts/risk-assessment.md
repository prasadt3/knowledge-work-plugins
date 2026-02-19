---
name: risk-assessment
description: |
  Produce a focused risk analysis for a stock or group of stocks. Use after collecting data from
  run_equity_analysis_tool (for financial health metrics) and get_equity_snapshot_tool (for
  volatility, beta, and analyst spread). Produces a structured risk profile covering quantitative
  risk metrics, qualitative risk factors, and scenario analysis.
tools-required:
  - mcp__agentman-alpha__run_equity_analysis_tool
  - mcp__agentman-alpha__get_equity_snapshot_tool
estimated-time: 1-2 min
output-format: PDF or DOCX titled "Agentman — Risk Assessment", authored by "Agentman Equity Research Assistant"
---

# Risk Assessment

You are producing a focused risk analysis. The goal is to identify, quantify, and contextualize the risks of owning this stock — both the measurable (quantitative) and the judgmental (qualitative).

## Data Extraction

### Quantitative Risk Metrics (from tools)
- [ ] Beta (systematic risk relative to market)
- [ ] Annualized volatility
- [ ] 52-week range and % from high (drawdown potential)
- [ ] Current ratio (liquidity risk)
- [ ] Debt levels: total debt, net debt, debt/equity if available
- [ ] Free cash flow trend (cash generation reliability)
- [ ] Revenue concentration (single product/segment dependency)
- [ ] Analyst price target spread (high - low = uncertainty level)
- [ ] Sell rating count (bear conviction)

### Qualitative Risk Factors (from your knowledge + news)
- Competitive dynamics
- Regulatory environment
- Geopolitical exposure
- Technology disruption risk
- Management/execution risk
- Customer/supplier concentration

## Report Structure

### Header
```
# Agentman — Risk Assessment: {Company Name} ({TICKER})

**Date**: {date} | **Price**: ${price} | **Beta**: {beta}
**Analyst**: Agentman Equity Research Assistant
```

### Section 1: Risk Summary
A single-paragraph, 3-4 sentence overview of the stock's risk profile. Characterize it as:
- **Low Risk**: Stable cash flows, low leverage, defensive sector, low beta
- **Moderate Risk**: Some concentration, cyclical exposure, average leverage
- **Elevated Risk**: High leverage, execution uncertainty, competitive pressure, high beta
- **High Risk**: Pre-profit, binary outcomes, heavy debt, regulatory overhang

### Section 2: Quantitative Risk Profile

| Risk Metric | Value | Assessment |
|-------------|-------|------------|
| **Beta** | {value} | {< 0.8 = defensive, 0.8-1.2 = market-like, > 1.2 = aggressive} |
| **Annualized Volatility** | {pct}% | {< 20% = low, 20-35% = moderate, > 35% = high} |
| **52-Week Drawdown** | {pct from high}% | {< 10% = near highs, 10-25% = correction, > 25% = significant} |
| **Current Ratio** | {value} | {> 1.5 = strong, 1.0-1.5 = adequate, < 1.0 = monitor} |
| **Net Debt** | ${value}B | {Negative = net cash, positive = leveraged} |
| **FCF Trend** | {direction} | {Growing = healthy, declining = concern} |
| **Analyst PT Spread** | ${low} - ${high} | {Wide = high uncertainty, narrow = consensus} |
| **Sell Ratings** | {count} of {total} | {0 = no bears, >10% = notable skepticism} |

### Section 3: Qualitative Risk Factors

Rate each factor and provide a specific explanation:

#### Company-Specific Risks
| Risk Factor | Severity | Description |
|-------------|----------|-------------|
| Revenue Concentration | {Low/Med/High} | {e.g., "iPhone is ~50% of Apple's revenue"} |
| Competitive Position | {Low/Med/High} | {e.g., "Dominant market share but facing Huawei in China"} |
| Management/Execution | {Low/Med/High} | {e.g., "Proven management team, 10+ year CEO tenure"} |
| Innovation Pipeline | {Low/Med/High} | {e.g., "Vision Pro uncertain, AI integration still early"} |

#### Industry Risks
| Risk Factor | Severity | Description |
|-------------|----------|-------------|
| Regulatory | {Low/Med/High} | {e.g., "EU DMA compliance, US DOJ antitrust scrutiny"} |
| Disruption | {Low/Med/High} | {e.g., "AI-native competitors emerging in search"} |
| Cyclicality | {Low/Med/High} | {e.g., "Consumer electronics sensitive to economic cycles"} |

#### Macro Risks
| Risk Factor | Severity | Description |
|-------------|----------|-------------|
| Interest Rate Sensitivity | {Low/Med/High} | {How rates affect valuation and operations} |
| Geopolitical Exposure | {Low/Med/High} | {Geographic revenue breakdown, supply chain} |
| Currency Risk | {Low/Med/High} | {International revenue exposure, hedging} |

### Section 4: Scenario Analysis

Present three scenarios with probability-weighted outcomes:

| Scenario | Probability | Price Implication | Key Driver |
|----------|-------------|-------------------|------------|
| **Bull Case** | {pct}% | ${target} ({+pct}%) | {Primary catalyst} |
| **Base Case** | {pct}% | ${target} ({+/-pct}%) | {Status quo assumption} |
| **Bear Case** | {pct}% | ${target} ({-pct}%) | {Primary risk} |

Guidelines for scenarios:
- **Bull**: Analyst high target or above if strong catalysts exist
- **Base**: Near analyst median target
- **Bear**: Analyst low target or fundamental support level
- Probabilities should sum to 100% and reflect current positioning

### Section 4.5: Risk Tolerance by Investor Profile

Map the risk findings to each investor profile's tolerance thresholds:

| Risk Dimension | Value | Conservative Tolerance | Moderate Tolerance | Aggressive Tolerance |
|----------------|-------|----------------------|-------------------|---------------------|
| **Beta** | {value} | < 1.0 {Pass/Fail} | 0.8-1.3 {Pass/Fail} | > 1.2 OK {Pass/Fail} |
| **Volatility** | {pct}% | < 20% {Pass/Fail} | 20-30% {Pass/Fail} | 30%+ OK {Pass/Fail} |
| **Max Drawdown** | {pct}% | < 15% {Pass/Fail} | 15-25% {Pass/Fail} | 30%+ OK {Pass/Fail} |
| **Leverage** | {D/E ratio} | < 0.6 {Pass/Fail} | < 1.0 {Pass/Fail} | < 1.5 {Pass/Fail} |

**Risk Profile Summary by Investor Type**:
- **Conservative**: {Pass/Fail count} of 4 thresholds met. {1-sentence: "Risk profile is [compatible/incompatible] — [primary concern or strength]."}
- **Moderate**: {Pass/Fail count} of 4 thresholds met. {1-sentence assessment.}
- **Aggressive**: {Pass/Fail count} of 4 thresholds met. {1-sentence assessment.}

### Section 5: Risk Mitigants
3-4 bullets on factors that reduce risk:
- **{Mitigant}**: {How it protects downside — e.g., buyback floor, dividend support, cash reserves, diversified revenue}

### Section 6: Key Risk Monitoring Triggers
Specific thresholds or events that would signal elevated risk:
- "{Metric} drops below {threshold}" — {implication}
- "{Event} occurs" — {expected impact}
- "{Competitor} achieves {milestone}" — {competitive threat}

### Disclaimer
> *This Agentman risk assessment is for informational purposes only and does not constitute personalized investment advice. Risk assessments are inherently uncertain and actual outcomes may differ materially from scenarios presented. Investors should conduct their own due diligence and consult a licensed financial advisor. Prepared by Agentman Equity Research Assistant.*

## Analysis Guidelines
- Quantify wherever possible: "China represents ~20% of revenue" > "China is a significant market"
- Be honest about uncertainty: If a risk is truly unknowable, say so rather than assigning false precision
- Distinguish between permanent risks (capital loss) and temporary risks (volatility)
- The most important risks are often the ones no one is talking about — think about tail risks
- Don't just list risks — assess their probability AND impact. A high-probability/low-impact risk is different from a low-probability/catastrophic risk

## Brand Color Reference

All reports are output as **PDF or DOCX** (user's choice, PDF by default). Title: **"Agentman — Risk Assessment"** (set in document metadata and cover page). Author: **Agentman Equity Research Assistant** (display in header/cover and footer). For DOCX, use `python-docx` with brand colors applied via `RGBColor`, table cell shading, and custom styles. Apply the Agentman brand palette from `references/brand-colors.md`, following the **agentman-pptx-style** design system.

- **Visual weight**: 70% Carbon/Charcoal, 20% Warm Neutrals, 10% Terracotta accent
- **Section titles**: `CHARCOAL_900` (#292322) with `AGENTMAN_500` (#CC785C) underline
- **Body text**: `CHARCOAL_950` (#141413); secondary `SLATE_600` (#475569)
- **Table headers**: `AGENTMAN_100` (#F6EAE6) light fill, `AGENTMAN_500` (#CC785C) terracotta text
- **Table borders**: `AGENTMAN_150` (#E3DACC) warm
- **Alternating table rows**: `AGENTMAN_50` (#FAF9F5) cream / white
- **Low Risk / defensive**: `AGENTMAN_500` (#CC785C) terracotta (positive emphasis)
- **High Risk / elevated**: `AGENTMAN_600` (#A65945) deep terracotta bold
- **Moderate Risk / mixed**: `CHARCOAL_950` (#141413) bold
- **Severity column** (Low/Med/High): terracotta / charcoal bold / deep terracotta respectively
- **Bull scenario row**: `AGENTMAN_500` terracotta accent
- **Bear scenario row**: `AGENTMAN_600` deep terracotta accent
- **Base scenario row**: `CHARCOAL_950` bold
- **Risk mitigants**: `AGENTMAN_500` terracotta to signal downside protection

**BANNED**: Green, red, amber, blue (except ✓/✗ comparison symbols). No gradients. No invented colors. See `references/color-antipatterns.md`.
