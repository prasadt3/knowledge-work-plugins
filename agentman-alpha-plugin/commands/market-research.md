---
allowed-tools: mcp__agentman-alpha__run_market_analysis_tool, mcp__agentman-alpha__compare_stocks_tool, mcp__agentman-alpha__get_equity_snapshot_tool
description: Understand a company's competitive position with SWOT analysis and market intelligence
argument-hint: <TICKER or sector>
---

Conduct competitive intelligence and strategic market analysis for a stock or sector.

## Your task

1. If $ARGUMENTS is provided, use it as the ticker symbol or sector name. Otherwise, ask the user what company or sector to analyze.

2. Gather data using the available tools:
   - Call `mcp__agentman-alpha__run_market_analysis_tool` for the primary ticker to get company profile, financials, ratings, and news context
   - If competitors are identifiable from the profile, call `mcp__agentman-alpha__compare_stocks_tool` with the ticker and 2-4 key competitors
   - Optionally call `mcp__agentman-alpha__get_equity_snapshot_tool` for quick metrics on individual competitors

3. Synthesize the data into a **Market Intelligence Report** with these sections:

   ## Company Profile
   Brief description, sector, market cap, key business segments.

   ## SWOT Analysis
   | | Positive | Negative |
   |---|---|---|
   | **Internal** | **Strengths**: ... | **Weaknesses**: ... |
   | **External** | **Opportunities**: ... | **Threats**: ... |

   ## Competitive Positioning
   How the company ranks vs. peers on key metrics (valuation, growth, profitability, momentum). Include a comparison table if data is available.

   ## Industry Dynamics
   Key trends, headwinds, and tailwinds affecting the sector. Regulatory environment.

   ## Recent Catalysts
   Key headlines and events from news data that may impact competitive positioning.

   ## Strategic Outlook
   Near-term and long-term positioning assessment. Key factors to monitor.

4. End with the disclaimer:
   > *This research is for informational purposes only and does not constitute personalized investment advice. Past performance does not guarantee future results.*

5. **Apply Agentman brand colors** per `references/brand-colors.md`, following the **agentman-pptx-style** design system: `AGENTMAN_100` (#F6EAE6) light fill table headers with `AGENTMAN_500` (#CC785C) terracotta text, `AGENTMAN_150` (#E3DACC) warm borders, charcoal text (#141413), `AGENTMAN_500` for strengths/opportunities, `AGENTMAN_600` (#A65945) for weaknesses/threats, `CHARCOAL_950` bold for moderate forces, cream alternating rows (#FAF9F5). Green/red/amber/blue are **BANNED** (except ✓/✗ symbols).

6. **Deliver as a PDF or DOCX file** (user's choice, PDF by default). Use Python to generate a styled **PDF** (e.g., `reportlab`, `fpdf2`, `weasyprint`) or **DOCX** (e.g., `python-docx`) with Agentman brand colors, set document author to "Agentman Equity Research Assistant" and title to "Agentman — {Report Title}", save to the filesystem, and provide the file path. For DOCX, apply brand colors via `RGBColor` font colors, table cell shading, and custom styles per `references/brand-colors.md`. **NEVER deliver as HTML.** If an intermediate HTML step is needed, delete it after conversion.

For a comprehensive planned research workflow with DCF valuation, suggest `/research <TICKER>`.
