---
allowed-tools: mcp__agentman-alpha__get_equity_snapshot_tool, mcp__agentman-alpha__run_market_analysis_tool, mcp__agentman-alpha__run_equity_analysis_tool, mcp__agentman-alpha__compare_stocks_tool, mcp__agentman-alpha__get_valuation_tool
description: Get a structured equity research report — you approve the plan before data collection begins
argument-hint: <TICKER or research question>
---

Conduct comprehensive equity research using a two-phase planning-first workflow.

## Your task

### Phase 1: Create Research Plan

1. If $ARGUMENTS is provided, parse it to identify ticker symbol(s) and research intent. Otherwise, ask the user what they'd like to research.

2. Analyze the request to determine the appropriate research depth:

| Signal | Depth | Tools to Plan |
|--------|-------|---------------|
| "Quick check", "how is X doing" | Quick (~30s) | `get_equity_snapshot_tool` |
| Single ticker, general question | Standard (~2-3 min) | `run_equity_analysis_tool` + `run_market_analysis_tool` |
| "Full report", "deep dive", "research" | Comprehensive (~4-6 min) | All tools including `get_valuation_tool` |
| Multiple tickers, "compare" | Comparison (~1-2 min) | `compare_stocks_tool` + snapshots |
| "Is X overvalued?", "fair value" | Valuation (~2-4 min) | `get_valuation_tool` + `get_equity_snapshot_tool` |
| "SWOT", "competitive", "market research" | Market Intelligence (~1-2 min) | `run_market_analysis_tool` + `compare_stocks_tool` |
| "conservative", "moderate", "aggressive", "investor profile", "risk profile" | Profile Analysis (~3-5 min) | `get_equity_snapshot_tool` + `run_equity_analysis_tool` + `get_valuation_tool` |
| "comps", "comparable", "peer valuation", "relative valuation" | Comps Analysis (~1-3 min) | `get_equity_snapshot_tool` + `compare_stocks_tool` + `run_equity_analysis_tool` |
| "merton", "black-scholes", "default risk", "structural valuation" | Merton Model (~1-2 min) | `get_equity_snapshot_tool` + `run_equity_analysis_tool` |
| "advanced valuation", "comps and merton", "full valuation" | Advanced Valuation (~3-5 min) | `get_equity_snapshot_tool` + `run_equity_analysis_tool` + `compare_stocks_tool` |

3. Create a structured **Research Plan** and present it:

```
## Research Plan: [Topic]

**Scope**: [Quick Check / Standard Analysis / Comprehensive Report / Comparison / Valuation Focus / Market Intelligence]
**Estimated Time**: [total time]
**Ticker(s)**: [list]

| Step | Action | Tool | Purpose | Est. Time |
|------|--------|------|---------|-----------|
| 1 | ... | `tool_name` | ... | ~Xs |
| 2 | ... | `tool_name` | ... | ~Xs |

**Parallelization**: Steps X and Y will run simultaneously.
**Deliverable**: [description of output format]

Shall I proceed with this plan?
```

4. **STOP AND WAIT** for the user to approve, modify, or reject the plan. Do NOT proceed to Phase 2 until the user explicitly approves.

### Phase 2: Execute Plan

5. After user approval, execute the tools in the planned order:
   - Parallelize independent tool calls (e.g., `run_equity_analysis_tool` and `run_market_analysis_tool` for the same ticker)
   - Run sequential steps in order
   - Inform the user when starting slow tools (valuation takes 1-3 min)

6. Synthesize results into the appropriate output format:

**Quick Check Output:**
- Price, key metrics, analyst consensus in a compact summary
- One-sentence valuation assessment

**Standard Analysis Output:**
- Company Overview, Financial Performance, Valuation, Analyst Sentiment, Recent News, Bull/Bear Case, Summary

**Comprehensive Report Output:**
- Executive Summary, Company Overview, Financial Analysis, Market Context, Valuation Assessment, Risk Analysis, Investment Conclusion, Appendix

**Comparison Output:**
- Markdown comparison table, relative value analysis, standout picks

**Valuation Output:**
- Current Price vs. Intrinsic Value, Key Assumptions, Context, Caveats

**Market Intelligence Output:**
- SWOT Analysis, Competitive Positioning, Industry Dynamics, Strategic Outlook

**Profile Analysis Output:**
- Profile Scores Summary (Conservative, Moderate, Aggressive — each scored out of 50)
- Detailed score breakdowns per profile with sub-component scores
- Best Fit determination with rationale
- Cross-Profile Action Summary (verdict, position size, entry, time horizon per profile)
- Use the investor-profile-valuation prompt template and investor-profile-methodology skill scoring rubric

**Comps Analysis Output:**
- Peer group selection with justification
- Multiple comparison table (P/E, EV/EBITDA, P/S, P/B across target + peers)
- Implied valuations per multiple with weights
- Weighted fair value and range (25th-75th percentile)
- Premium/discount assessment
- Use the comparable-company-valuation prompt template and advanced-valuation-methodology skill

**Merton Model Output:**
- Model inputs table (market cap, debt, beta, derived volatilities)
- Step-by-step Black-Scholes computation with actual numbers
- Model vs. market comparison (Merton value vs. price, distance to default, default probability)
- Sensitivity analysis (volatility x maturity matrix, rate sensitivity)
- Use the merton-model-valuation prompt template and advanced-valuation-methodology skill

**Advanced Valuation Output:**
- Combined Comps + Merton sections (as above)
- Valuation synthesis table comparing methodologies
- Consensus fair value range across all available methodologies
- Use both prompt templates and the advanced-valuation-methodology skill

7. **Apply Agentman brand colors** following the **agentman-pptx-style** design system. Use the palette from `references/brand-colors.md`:
   - Visual weight: 70% Carbon/Charcoal, 20% Warm Neutrals, 10% Terracotta accent
   - Table headers: `AGENTMAN_100` (#F6EAE6) light fill + `AGENTMAN_500` (#CC785C) terracotta text
   - Table borders: `AGENTMAN_150` (#E3DACC) warm
   - Section titles: `CHARCOAL_900` (#292322) with `AGENTMAN_500` (#CC785C) underline
   - Body text: `CHARCOAL_950` (#141413)
   - Alternating table rows: `AGENTMAN_50` (#FAF9F5) cream / white
   - Highlight rows (totals, key metrics): `AGENTMAN_75` (#F0EEE6) warm cream
   - Emphasis text: `AGENTMAN_500` positive, `AGENTMAN_600` negative, `AGENTMAN_400` caution, `CHARCOAL_950` neutral bold
   - Verdict boxes: `AGENTMAN_500` border + `AGENTMAN_50` cream bg — same style for all
   - **BANNED**: Green, red, amber, blue (except ✓/✗ symbols). No gradients.

8. **Deliver the report as a PDF or DOCX file** (user's choice, PDF by default). Use Python to generate a styled **PDF** (e.g., `reportlab`, `fpdf2`, `weasyprint`) or **DOCX** (e.g., `python-docx`) with Agentman brand colors. Set document author to "Agentman Equity Research Assistant" and title to "Agentman — {Report Title}". For DOCX, apply brand colors via `RGBColor` font colors, table cell shading, and custom styles per `references/brand-colors.md`. Save to the filesystem and provide the file path. **NEVER deliver as an HTML file.** If an intermediate HTML step is needed for PDF conversion, delete the HTML after. **NEVER output the full report as inline markdown** when the user asks for a report — always produce a downloadable PDF or DOCX.

9. End every report with the disclaimer:
   > *This research is for informational purposes only and does not constitute personalized investment advice. Past performance does not guarantee future results. Investors should conduct their own due diligence and consult a licensed financial advisor.*
