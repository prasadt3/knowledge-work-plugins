---
allowed-tools: mcp__agentman-alpha__get_equity_snapshot_tool
description: Quick stock health check — key metrics and analyst sentiment at a glance
argument-hint: <TICKER>
---

Get a quick snapshot of the stock specified by the user.

## Your task

1. If $ARGUMENTS is provided, use it as the ticker symbol. Otherwise, ask the user for a ticker.
2. Call `mcp__agentman-alpha__get_equity_snapshot_tool` with the ticker symbol.
3. Present a concise summary covering:
   - **Price & Change**: Current price, daily change percentage
   - **Valuation**: P/E ratio, P/B ratio, forward P/E if available
   - **Profitability**: ROE, profit margins
   - **Dividends**: Yield and payout ratio if applicable
   - **Analyst Consensus**: Rating, price target, and upside/downside percentage
4. End with a one-sentence assessment of whether the stock looks attractively valued based on the metrics.

5. **Apply Agentman brand colors** per `references/brand-colors.md`, following the **agentman-pptx-style** design system: `AGENTMAN_100` (#F6EAE6) light fill table headers with `AGENTMAN_500` (#CC785C) terracotta text, `AGENTMAN_150` (#E3DACC) warm borders, charcoal text (#141413), `AGENTMAN_500` for positive emphasis, `AGENTMAN_600` (#A65945) for negative emphasis, cream alternating rows (#FAF9F5). Green/red/amber/blue are **BANNED** (except ✓/✗ symbols).

6. **Deliver as a PDF or DOCX file** (user's choice, PDF by default). Use Python to generate a styled **PDF** (e.g., `reportlab`, `fpdf2`, `weasyprint`) or **DOCX** (e.g., `python-docx`) with Agentman brand colors, set document author to "Agentman Equity Research Assistant" and title to "Agentman — {Report Title}", save to the filesystem, and provide the file path. For DOCX, apply brand colors via `RGBColor` font colors, table cell shading, and custom styles per `references/brand-colors.md`. **NEVER deliver as HTML.** If an intermediate HTML step is needed, delete it after conversion.

For comprehensive analysis with a research plan, use `/research <TICKER>`.
