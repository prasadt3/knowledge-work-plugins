---
allowed-tools: mcp__agentman-alpha__compare_stocks_tool, mcp__agentman-alpha__get_equity_snapshot_tool
description: Compare 2-5 stocks side by side on valuation, growth, and risk
argument-hint: <TICKER1,TICKER2,...>
---

Compare multiple stocks side by side with key metrics.

## Your task

1. If $ARGUMENTS is provided, use it as the comma-separated list of ticker symbols. Otherwise, ask the user for 2-5 ticker symbols.

2. Call `mcp__agentman-alpha__compare_stocks_tool` with the comma-separated symbols.

3. Present the comparison as a markdown table with columns for each stock and rows for:
   - Price
   - Market Cap
   - P/E Ratio
   - P/B Ratio
   - ROE
   - Dividend Yield
   - 1-Month Return
   - 3-Month Return
   - 1-Year Return
   - Volatility
   - Analyst Rating

4. Below the table, provide a brief analysis:
   - Which stock has the best value (lowest P/E relative to growth)?
   - Which has the strongest momentum (best returns)?
   - Which has the best profitability (highest ROE, margins)?
   - Which carries the most risk (highest volatility)?

5. End with a one-paragraph summary of which stock(s) stand out and why.

6. **Apply Agentman brand colors** per `references/brand-colors.md`, following the **agentman-pptx-style** design system: `AGENTMAN_100` (#F6EAE6) light fill table headers with `AGENTMAN_500` (#CC785C) terracotta text, `AGENTMAN_150` (#E3DACC) warm borders, charcoal text (#141413), `AGENTMAN_500` for winner/leader values, `AGENTMAN_600` (#A65945) for laggard values, cream alternating rows (#FAF9F5). Green/red/amber/blue are **BANNED** (except ✓/✗ symbols).

7. **Deliver as a PDF or DOCX file** (user's choice, PDF by default). Use Python to generate a styled **PDF** (e.g., `reportlab`, `fpdf2`, `weasyprint`) or **DOCX** (e.g., `python-docx`) with Agentman brand colors, set document author to "Agentman Equity Research Assistant" and title to "Agentman — {Report Title}", save to the filesystem, and provide the file path. For DOCX, apply brand colors via `RGBColor` font colors, table cell shading, and custom styles per `references/brand-colors.md`. **NEVER deliver as HTML.** If an intermediate HTML step is needed, delete it after conversion.

For comprehensive analysis with a research plan, use `/research <TICKER1,TICKER2,...>`.
