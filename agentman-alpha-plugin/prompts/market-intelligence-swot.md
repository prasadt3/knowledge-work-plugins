---
name: market-intelligence-swot
description: |
  Produce a competitive intelligence and strategic analysis report including SWOT analysis,
  Porter's Five Forces assessment, and competitive positioning. Use after collecting data from
  run_market_analysis_tool and optionally compare_stocks_tool with key competitors.
tools-required:
  - mcp__agentman-alpha__run_market_analysis_tool
  - mcp__agentman-alpha__compare_stocks_tool (optional, for peer comparison)
  - mcp__agentman-alpha__get_equity_snapshot_tool (optional, for competitor snapshots)
estimated-time: 1-2 min
output-format: PDF or DOCX titled "Agentman — Market Intelligence & SWOT Analysis", authored by "Agentman Equity Research Assistant"
---

# Market Intelligence & SWOT Analysis

You are producing a strategic market intelligence report. Combine quantitative data from tools with your knowledge of the company's competitive landscape, industry dynamics, and strategic positioning.

## Data Extraction

### From Market Analysis Tool
- [ ] Company profile (description, sector, industry, employees, CEO)
- [ ] Current financials (revenue, margins, growth)
- [ ] Analyst sentiment and price targets
- [ ] Recent news headlines and themes

### From Compare Tool (if competitors included)
- [ ] Relative valuation metrics
- [ ] Relative profitability
- [ ] Relative performance and momentum
- [ ] Relative analyst sentiment

## Report Structure

### Header
```
# Agentman — Market Intelligence Report: {Company Name} ({TICKER})

**Date**: {date} | **Sector**: {sector} | **Industry**: {industry}
**Analyst**: Agentman Equity Research Assistant
```

### Section 1: Company Profile
2-3 sentence overview covering:
- What the company does (core business segments)
- Market position (leader, challenger, niche player)
- Scale (revenue, employees, market cap)

### Section 2: SWOT Analysis

Present as a 2x2 grid:

```
### Strengths (Internal, Positive)
- **{Label}**: 1-sentence explanation with data
- **{Label}**: ...
- **{Label}**: ...

### Weaknesses (Internal, Negative)
- **{Label}**: 1-sentence explanation with data
- **{Label}**: ...
- **{Label}**: ...

### Opportunities (External, Positive)
- **{Label}**: 1-sentence explanation
- **{Label}**: ...
- **{Label}**: ...

### Threats (External, Negative)
- **{Label}**: 1-sentence explanation
- **{Label}**: ...
- **{Label}**: ...
```

Guidelines for each quadrant:
- **Strengths**: Focus on competitive advantages backed by financial data (margins, market share, brand, IP, scale, cash flow)
- **Weaknesses**: Identify operational gaps, financial vulnerabilities, concentration risks, strategic blind spots
- **Opportunities**: Cover market expansion, new products, AI/tech adoption, M&A, favorable regulation, demographic trends
- **Threats**: Cover competitive pressure, disruption risk, regulatory headwinds, geopolitical exposure, macro sensitivity

Aim for 3-5 items per quadrant. Each item must be specific and actionable, not generic.

### Section 3: Porter's Five Forces Assessment

Rate each force as **Low**, **Moderate**, or **High** with a brief explanation:

| Force | Rating | Assessment |
|-------|--------|------------|
| Threat of New Entrants | {Low/Mod/High} | {Why — barriers to entry, capital requirements, regulatory moats} |
| Supplier Power | {Low/Mod/High} | {Why — supplier concentration, switching costs, vertical integration} |
| Buyer Power | {Low/Mod/High} | {Why — customer concentration, price sensitivity, alternatives} |
| Threat of Substitutes | {Low/Mod/High} | {Why — substitute availability, switching costs, performance gap} |
| Competitive Rivalry | {Low/Mod/High} | {Why — number of competitors, differentiation, price competition} |

**Overall Industry Attractiveness**: {Favorable / Neutral / Challenging} — 1-2 sentence summary.

### Section 4: Competitive Positioning (if peer data available)

#### Peer Comparison Table
| Metric | {TICKER} | Peer 1 | Peer 2 | Peer 3 |
|--------|----------|--------|--------|--------|
| Market Cap | ... | ... | ... | ... |
| Revenue | ... | ... | ... | ... |
| Operating Margin | ... | ... | ... | ... |
| Net Margin | ... | ... | ... | ... |
| 3M Return | ... | ... | ... | ... |
| Analyst Consensus | ... | ... | ... | ... |

#### Competitive Advantages
Bulleted list of 3-4 specific competitive advantages the subject company has over peers.

#### Competitive Vulnerabilities
Bulleted list of 2-3 areas where competitors have an edge.

### Section 5: Recent Catalysts & News
Summarize 3-5 key recent developments from the news data:
- **{Headline theme}**: 1-sentence impact assessment (positive/negative/neutral catalyst)

### Section 6: Strategic Outlook

#### Near-Term (6-12 months)
2-3 sentences on the most likely developments, catalysts, and risks in the near term.

#### Long-Term (2-5 years)
2-3 sentences on structural trends, strategic pivots, and secular tailwinds/headwinds.

#### Key Monitoring Triggers
Bulleted list of 3-5 specific events or metrics to watch:
- "{Specific event or metric threshold}" — {why it matters}

### Disclaimer
> *This Agentman market intelligence report is for informational purposes only and does not constitute personalized investment advice. Past performance does not guarantee future results. Investors should conduct their own due diligence and consult a licensed financial advisor. Prepared by Agentman Equity Research Assistant.*

## Analysis Guidelines
- Leverage your knowledge of the industry to fill in competitive context beyond what the data tools provide
- Be specific: "Apple's 47% gross margin reflects its premium pricing power" NOT "Apple has good margins"
- Differentiate between cyclical and structural factors
- For SWOT, avoid generic items like "strong brand" — specify what the brand enables (pricing power, customer retention, talent attraction)
- When rating Porter's forces, anchor to the specific industry, not general business

## Brand Color Reference

All reports are output as **PDF or DOCX** (user's choice, PDF by default). Title: **"Agentman — Market Intelligence & SWOT Analysis"** (set in document metadata and cover page). Author: **Agentman Equity Research Assistant** (display in header/cover and footer). For DOCX, use `python-docx` with brand colors applied via `RGBColor`, table cell shading, and custom styles. Apply the Agentman brand palette from `references/brand-colors.md`, following the **agentman-pptx-style** design system.

- **Visual weight**: 70% Carbon/Charcoal, 20% Warm Neutrals, 10% Terracotta accent
- **Section titles**: `CHARCOAL_900` (#292322) with `AGENTMAN_500` (#CC785C) underline
- **Body text**: `CHARCOAL_950` (#141413); secondary `SLATE_600` (#475569)
- **Table headers**: `AGENTMAN_100` (#F6EAE6) light fill, `AGENTMAN_500` (#CC785C) terracotta text
- **Table borders**: `AGENTMAN_150` (#E3DACC) warm
- **Alternating table rows**: `AGENTMAN_50` (#FAF9F5) cream / white
- **Strengths / Opportunities** (positive): `AGENTMAN_500` (#CC785C) terracotta accent
- **Weaknesses / Threats** (negative): `AGENTMAN_600` (#A65945) deep terracotta accent
- **Porter's Forces "Low"** (favorable): `AGENTMAN_500` terracotta; **"High"** (unfavorable): `AGENTMAN_600` deep terracotta; **"Moderate"**: `CHARCOAL_950` bold
- **Industry Attractiveness**: Use terracotta emphasis scale, not semantic colors
- **News catalysts**: positive in `AGENTMAN_500`, negative in `AGENTMAN_600`, neutral in `SLATE_600` (#475569)
- **Terracotta budget**: max 3 `AGENTMAN_500` elements per section

**BANNED**: Green, red, amber, blue (except ✓/✗ comparison symbols). No gradients. No invented colors. See `references/color-antipatterns.md`.
