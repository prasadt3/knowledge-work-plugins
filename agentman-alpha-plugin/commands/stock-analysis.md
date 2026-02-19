---
allowed-tools: mcp__agentman-alpha__run_equity_analysis_tool, mcp__agentman-alpha__run_market_analysis_tool, mcp__agentman-alpha__get_valuation_tool
description: Get a comprehensive equity analysis — financials, valuation, and investment thesis in one report
argument-hint: <TICKER>
---

Generate a comprehensive equity analysis report for the given stock.

## Your task

1. If $ARGUMENTS is provided, use it as the ticker symbol. Otherwise, ask the user for a ticker.

2. Run these two tools in parallel to gather data:
   - `mcp__agentman-alpha__run_equity_analysis_tool` for comprehensive financials, ratios, price performance, and analyst ratings
   - `mcp__agentman-alpha__run_market_analysis_tool` for company profile, current quote, recent news, and market context

3. After reviewing the data from steps above, run `mcp__agentman-alpha__get_valuation_tool` for a DCF intrinsic value estimate. Note: this takes 1-3 minutes.

4. Synthesize all data into a structured research report with these sections:

   ## Company Overview
   Brief description, sector, market cap, key business segments.

   ## Financial Performance
   Revenue trends, earnings growth, margins, and profitability metrics.

   ## Valuation
   Current P/E, P/B, and other multiples vs. sector averages. Include the DCF-derived intrinsic value vs. current price.

   ## Analyst Sentiment
   Consensus rating, price targets, and recent rating changes.

   ## Recent News & Catalysts
   Key headlines and events that may impact the stock.

   ## Bull Case / Bear Case
   3 bullet points for each side.

   ## Summary
   One-paragraph investment thesis with a clear stance (undervalued, fairly valued, or overvalued).

5. **Apply Agentman brand colors** per `references/brand-colors.md`, following the **agentman-pptx-style** design system: `AGENTMAN_100` (#F6EAE6) light fill table headers with `AGENTMAN_500` (#CC785C) terracotta text, `AGENTMAN_150` (#E3DACC) warm borders, charcoal text (#141413), `AGENTMAN_500` for positive emphasis, `AGENTMAN_600` (#A65945) for negative emphasis, cream alternating rows (#FAF9F5). Green/red/amber/blue are **BANNED** (except ✓/✗ symbols).

6. **Deliver as a PDF or DOCX file** (user's choice, PDF by default). Use Python to generate a styled **PDF** (e.g., `reportlab`, `fpdf2`, `weasyprint`) or **DOCX** (e.g., `python-docx`) with Agentman brand colors, set document author to "Agentman Equity Research Assistant" and title to "Agentman — {Report Title}", save to the filesystem, and provide the file path. For DOCX, apply brand colors via `RGBColor` font colors, table cell shading, and custom styles per `references/brand-colors.md`. **NEVER deliver as HTML.** If an intermediate HTML step is needed, delete it after conversion.

For a planning-first workflow where you approve each step before execution, use `/research <TICKER>`.
