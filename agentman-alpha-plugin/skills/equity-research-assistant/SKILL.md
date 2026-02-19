---
name: equity-research-assistant
description: |
  Use when coordinating comprehensive equity research across multiple specialist agents. Provides routing logic, report templates, compliance guardrails, and synthesis methodology — so you can combine data from multiple sources into clear, actionable investment reports.
---

This skill guides the orchestration of comprehensive equity research by coordinating specialist sub-agents and synthesizing their outputs into professional reports.

## Routing Logic

Determine which specialist(s) to invoke based on the user's request:

### Single-Agent Routing
- **"What's AAPL worth?"** -> StockAnalysisSpecialist (valuation focus)
- **"How's the tech sector doing?"** -> market-analyst-pro (sector analysis)
- **"Show me NVDA's latest earnings"** -> FinancialDataSpecialist (data retrieval)
- **"What's the competitive landscape?"** -> MarketIntelligenceAnalyst (strategic analysis)

### Multi-Agent Coordination
- **"Full research report on META"** -> All specialists in sequence
- **"Best semiconductor stock to buy"** -> market-analyst-pro -> StockAnalysisSpecialist
- **"Analyze my portfolio vs. the market"** -> FinancialDataSpecialist -> market-analyst-pro

### Coordination Sequence (for comprehensive reports)
1. **FinancialDataSpecialist** - Gather current data and fundamentals
2. **MarketIntelligenceAnalyst** - Provide market context and competitive positioning
3. **market-analyst-pro** - Provide sector context and comparisons
4. **StockAnalysisSpecialist** - Deliver valuations with full context

## Report Templates

### Quick Analysis
1. **Key Takeaway**: 2-3 sentence summary with rating
2. **Current Data**: Price, valuation, key metrics
3. **Analysis**: Core findings from relevant specialist
4. **Risks**: Primary concerns

### Comprehensive Research Report
1. **Executive Summary** - Investment thesis, rating, key catalysts and risks
2. **Company/Sector Overview** - Business description, market position, developments
3. **Financial Analysis** - Financials, earnings, balance sheet highlights
4. **Market Context** - Sector performance, peer comparison, macro factors
5. **Valuation Assessment** - Fair value, technical levels, bull/base/bear scenarios
6. **Risk Analysis** - Company-specific, sector, market risks
7. **Investment Conclusion** - Rating, price target, time horizon, triggers
8. **Appendix** - Detailed tables, methodology, sources

### Comparative Analysis Report
1. **Comparison Summary**: Rankings with rationale
2. **Side-by-Side Metrics**: All securities compared
3. **Individual Assessments**: Brief analysis of each
4. **Relative Value**: Best risk/reward
5. **Recommendation**: Preferred choice with reasoning

## Output Delivery — PDF and DOCX

**All reports MUST be delivered as PDF or DOCX files. NEVER output reports as HTML files.** When producing any report:
1. Generate a styled **PDF** (using `reportlab`, `fpdf2`, or `weasyprint`) or **DOCX** (using `python-docx`) with the Agentman brand palette, based on user preference. Default to **PDF** if no preference is stated.
2. Set document metadata: author = "Agentman Equity Research Assistant", title = "Agentman — {Report Title}" (e.g., "Agentman — Comprehensive Equity Report: AAPL")
3. For **DOCX**: apply Agentman brand colors via `python-docx` — custom font colors (`RGBColor`), table cell shading, paragraph borders, and style definitions using the hex values from `references/brand-colors.md`. Use the same 70/20/10 visual weight and all element-to-color mappings.
4. Save to the filesystem and provide the file path to the user
5. If an intermediate HTML step is needed for PDF conversion, delete the HTML file after conversion
6. NEVER deliver the full report as inline markdown when the user requests a report

## Synthesis Methodology

When combining outputs from multiple specialists:
- **Resolve conflicting assessments** with balanced analysis explaining both perspectives
- **Ensure consistent formatting** and terminology across sections
- **Highlight key takeaways** and actionable insights prominently
- **Lead with conclusions**, then support with evidence
- **Use specific numbers** and cite data sources

## Compliance Guardrails

### Required Practices
- Follow Reg FD standards
- Document all research with verifiable sources
- Disclose data sources and methodology limitations
- Flag potential conflicts of interest

### Required Disclaimers (include in every report)
- "This Agentman research report is for informational purposes only and does not constitute personalized investment advice."
- "Past performance does not guarantee future results."
- "Investors should conduct their own due diligence and consult a licensed financial advisor."
- "Prepared by Agentman Equity Research Assistant."

### Prohibited Actions
- Personalized investment advice for individual circumstances
- Executing trades or guaranteeing outcomes
- Sharing client information with unauthorized parties

## Brand Color & Styling (Default for All Reports)

All reports (PDF and DOCX) MUST use the Agentman brand palette from `references/brand-colors.md`, following the **agentman-pptx-style** design system. Quiet confidence — charcoal suits, not fire trucks. See `references/color-antipatterns.md` for forbidden patterns.

- **Visual weight**: 70% Carbon/Charcoal, 20% Warm Neutrals, 10% Terracotta accent. Max 3 `AGENTMAN_500` elements per section.
- **Table headers**: `AGENTMAN_100` (#F6EAE6) light fill + `AGENTMAN_500` (#CC785C) terracotta text
- **Table borders**: `AGENTMAN_150` (#E3DACC) warm borders
- **Body text**: `CHARCOAL_950` (#141413); secondary `SLATE_600` (#475569)
- **Section underlines**: `AGENTMAN_500` (#CC785C); alternating rows: `AGENTMAN_50` cream / white; highlight rows: `AGENTMAN_75` warm cream
- **Emphasis text** (replaces semantic colors): `AGENTMAN_500` positive, `AGENTMAN_600` negative, `AGENTMAN_400` caution, `CHARCOAL_950` neutral
- **Badges**: Muted `AGENTMAN_100` bg + `AGENTMAN_800` text + `AGENTMAN_200` border. No color-coded tiers.
- **Callout blocks**: `AGENTMAN_75` cream bg + `CHARCOAL_950` heading + `SLATE_600` body
- **Score bars**: `AGENTMAN_150` track + `AGENTMAN_500` terracotta fill — same for all tiers
- **BANNED**: Green, red, amber, blue anywhere (except ✓/✗ comparison symbols). No gradients. No invented colors. No colored headings.

## Quality Standards
- **Accuracy**: Verify data consistency across sources
- **Timeliness**: Note data timestamps and freshness
- **Completeness**: Address all requested aspects
- **Clarity**: Use plain language; define technical terms
- **Actionability**: Include clear next steps in every report
