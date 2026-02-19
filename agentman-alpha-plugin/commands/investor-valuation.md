---
allowed-tools: mcp__agentman-alpha__get_equity_snapshot_tool, mcp__agentman-alpha__run_equity_analysis_tool, mcp__agentman-alpha__get_valuation_tool
description: See how a stock scores for Conservative, Moderate, and Aggressive investor profiles
argument-hint: <TICKER> [conservative|moderate|aggressive]
---

Evaluate a stock across investor risk profiles using a structured scoring methodology.

## Your task

1. **Parse arguments**: If $ARGUMENTS is provided, extract the ticker symbol and optional profile preference (conservative, moderate, or aggressive). If no ticker is provided, ask the user.

2. **Determine scope**:
   - If a specific profile is requested (e.g., `/investor-valuation AAPL conservative`), score all three profiles but emphasize the requested one in the output.
   - If no profile is specified, present a brief overview of the three profiles and ask the user to choose, or proceed with all three:

   ```
   Which investor profile would you like to evaluate {TICKER} against?

   1. **Conservative** — Capital preservation & income focus (dividend yield, low volatility, margin of safety)
   2. **Moderate** — Balanced growth + value (PEG ratio, profitability, analyst consensus)
   3. **Aggressive** — Growth & momentum focus (revenue acceleration, disruption potential, upside targets)
   4. **All three** — Complete profile comparison (recommended)

   Or I can proceed with all three profiles for a complete comparison.
   ```

   If the user doesn't respond within a reasonable conversational turn, default to all three.

3. **Collect data** — Run these tools, parallelizing where possible:
   - `mcp__agentman-alpha__get_equity_snapshot_tool(symbol)` — Quick metrics baseline (~10s)
   - `mcp__agentman-alpha__run_equity_analysis_tool(ticker)` — Comprehensive financials (~45s)
   - `mcp__agentman-alpha__get_valuation_tool(ticker)` — DCF intrinsic value (~1-3 min)

   Note: The valuation tool takes 1-3 minutes. Inform the user it's running.

   Run the snapshot and equity analysis tools in parallel. The valuation tool can also run in parallel with both.

4. **Score the stock** — Using the investor-profile-methodology skill, compute scores for each profile:

   **Conservative (50 pts)**: Dividend yield & consistency, balance sheet strength, earnings stability, valuation margin of safety, low volatility/beta

   **Moderate (50 pts)**: Growth-value balance / PEG, profitability quality, analyst consensus strength, reasonable valuation, risk-adjusted return potential

   **Aggressive (50 pts)**: Revenue growth rate, market position & TAM, momentum & technical strength, innovation/disruption potential, upside to price targets

5. **Present the results** using the investor-profile-valuation prompt template:
   - Profile Scores Summary (table with all 3 profiles)
   - Detailed score breakdowns (5 criteria per profile with sub-scores)
   - Best Fit determination
   - Cross-Profile Action Summary (verdict, position size, entry point, time horizon per profile)

6. **End with disclaimer**:
   > *This investor profile analysis is for informational purposes only and does not constitute personalized investment advice. Profile scores are based on quantitative screening criteria and do not account for individual financial situations, tax considerations, or complete portfolio context. Investors should conduct their own due diligence and consult a licensed financial advisor.*

7. **Apply Agentman brand colors** per `references/brand-colors.md`, following the **agentman-pptx-style** design system. `AGENTMAN_100` (#F6EAE6) light fill table headers with `AGENTMAN_500` (#CC785C) terracotta text, `AGENTMAN_150` (#E3DACC) warm borders, charcoal text (#141413), cream alternating rows (#FAF9F5). **Score badges**: `AGENTMAN_100` bg + `AGENTMAN_800` (#703B2D) text + `AGENTMAN_200` (#E6A890) border — no color-coded tiers, differentiation via text wording only. **Score bars**: `AGENTMAN_150` track + `AGENTMAN_500` terracotta fill — same for ALL tiers. **Verdicts**: Buy = `AGENTMAN_500` terracotta bold, Hold = `CHARCOAL_950` bold, Avoid = `AGENTMAN_600` (#A65945) deep terracotta bold. Green/red/amber/blue are **BANNED** (except ✓/✗ symbols).

8. **Deliver as a PDF or DOCX file** (user's choice, PDF by default). Use Python to generate a styled **PDF** (e.g., `reportlab`, `fpdf2`, `weasyprint`) or **DOCX** (e.g., `python-docx`) with Agentman brand colors, set document author to "Agentman Equity Research Assistant" and title to "Agentman — {Report Title}", save to the filesystem, and provide the file path. For DOCX, apply brand colors via `RGBColor` font colors, table cell shading, and custom styles per `references/brand-colors.md`. **NEVER deliver as HTML.** If an intermediate HTML step is needed, delete it after conversion.

For comprehensive research with market context and competitive analysis, use `/research <TICKER>`.
