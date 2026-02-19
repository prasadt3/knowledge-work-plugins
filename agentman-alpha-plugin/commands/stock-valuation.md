---
allowed-tools: mcp__agentman-alpha__get_valuation_tool, mcp__agentman-alpha__get_equity_snapshot_tool
description: Find out if a stock is overvalued or undervalued using a Damodaran DCF model
argument-hint: <TICKER>
---

Run a Discounted Cash Flow (DCF) valuation on a stock using the Damodaran methodology.

## Your task

1. If $ARGUMENTS is provided, use it as the ticker symbol. Otherwise, ask the user for a ticker.

2. Run both tools in parallel:
   - `mcp__agentman-alpha__get_equity_snapshot_tool` for current price and metrics context
   - `mcp__agentman-alpha__get_valuation_tool` for the DCF intrinsic value estimate

   Note: The valuation tool takes 1-3 minutes. Let the user know it is running.

3. Present the valuation results clearly:

   ## Valuation Summary
   - **Current Price**: from snapshot
   - **Estimated Intrinsic Value**: from DCF model
   - **Upside/Downside**: percentage difference
   - **Verdict**: Undervalued, Fairly Valued, or Overvalued

   ## Key Assumptions
   List the assumptions used by the model (revenue growth, operating margin, WACC, etc.).

   ## Context
   Compare the DCF value against current P/E, analyst price targets, and any other available valuation data points.

   ## Caveats
   Briefly note that DCF models are sensitive to input assumptions and should be one data point among many in an investment decision.

4. **Apply Agentman brand colors** per `references/brand-colors.md`, following the **agentman-pptx-style** design system: `AGENTMAN_100` (#F6EAE6) light fill table headers with `AGENTMAN_500` (#CC785C) terracotta text, `AGENTMAN_150` (#E3DACC) warm borders, charcoal text (#141413), `AGENTMAN_500` for undervalued emphasis, `AGENTMAN_600` (#A65945) for overvalued emphasis, `CHARCOAL_950` bold for fairly valued, cream alternating rows (#FAF9F5). Green/red/amber/blue are **BANNED** (except ✓/✗ symbols).

5. **Deliver as a PDF or DOCX file** (user's choice, PDF by default). Use Python to generate a styled **PDF** (e.g., `reportlab`, `fpdf2`, `weasyprint`) or **DOCX** (e.g., `python-docx`) with Agentman brand colors, set document author to "Agentman Equity Research Assistant" and title to "Agentman — {Report Title}", save to the filesystem, and provide the file path. For DOCX, apply brand colors via `RGBColor` font colors, table cell shading, and custom styles per `references/brand-colors.md`. **NEVER deliver as HTML.** If an intermediate HTML step is needed, delete it after conversion.

For comprehensive analysis with a research plan, use `/research <TICKER>`.
