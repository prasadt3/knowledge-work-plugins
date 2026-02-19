---
allowed-tools: mcp__agentman-alpha__get_equity_snapshot_tool, mcp__agentman-alpha__run_equity_analysis_tool, mcp__agentman-alpha__compare_stocks_tool
description: Value a stock from multiple angles — peer comps, Merton model, and/or asset-based NAV
argument-hint: <TICKER> [comps|merton|asset|all|both]
---

Perform advanced valuation analysis using Comparable Company Analysis (Comps), the Merton Model, and/or Asset-Based Valuation (Net Asset Value).

## Your task

1. Parse `$ARGUMENTS` to extract:
   - **Ticker**: The stock symbol (required). If missing, ask the user.
   - **Mode**: One of `comps`, `merton`, `asset`, `both`, or `all` (default: `all`). Accept variations: "comparable", "peer", "relative" map to `comps`; "black-scholes", "structural", "default risk" map to `merton`; "nav", "net-asset", "book-value", "liquidation", "asset-based" map to `asset`; `both` runs comps + merton (legacy); `all` runs comps + merton + asset.

2. Execute the appropriate workflow based on mode:

### Mode: `comps` (Comparable Company Analysis)

**Step 1**: Run `get_equity_snapshot_tool(symbol=TICKER)` to get target metrics.

**Step 2**: Identify 3-5 peer companies in the same sub-industry. Use your financial knowledge to select appropriate peers based on:
- Same sector/sub-industry
- Similar market cap range (0.3x to 3x)
- Similar business model

**Step 3**: Run `compare_stocks_tool(symbols="TICKER,PEER1,PEER2,PEER3[,PEER4,PEER5]")` to get side-by-side multiples.

**Step 4**: If more detailed data is needed for the target (e.g., EBITDA, book value, debt), run `run_equity_analysis_tool(ticker=TICKER)`.

**Step 5**: Synthesize using the **comparable-company-valuation** prompt template and the **advanced-valuation-methodology** skill for formulas and weighting.

### Mode: `merton` (Merton Model)

**Step 1**: Run `get_equity_snapshot_tool(symbol=TICKER)` and `run_equity_analysis_tool(ticker=TICKER)` **in parallel** to get market cap, beta, total debt, shares outstanding.

**Step 2**: Extract parameters: V (firm value), K (debt), sigma_E (equity vol from beta), sigma_V (asset vol), r (4.5%), T (5 years).

**Step 3**: Compute Black-Scholes: d1, d2, N(d1), N(d2), equity value, per-share value, default probability.

**Step 4**: Run sensitivity analysis across volatility, maturity, and rate variations.

**Step 5**: Synthesize using the **merton-model-valuation** prompt template and the **advanced-valuation-methodology** skill for formulas and interpretation.

### Mode: `asset` (Asset-Based Valuation)

**Step 1**: Run `get_equity_snapshot_tool(symbol=TICKER)` and `run_equity_analysis_tool(ticker=TICKER)` **in parallel** to get balance sheet data, market cap, shares outstanding, and P/B ratio.

**Step 2**: Extract balance sheet items: total assets, total liabilities, total equity, goodwill, intangible assets, PP&E, cash, receivables, inventory, current assets, current liabilities.

**Step 3**: Compute all valuation layers:
- Book Value per Share = Total Equity / Shares Outstanding
- Tangible Book Value per Share = (Total Equity - Goodwill - Intangibles) / Shares Outstanding
- Net-Net Working Capital per Share = (Current Assets - Total Liabilities) / Shares Outstanding
- Adjusted NAV per Share = (Sum of fair-value-adjusted assets - Total Liabilities) / Shares Outstanding

**Step 4**: Classify the company's asset profile (asset-heavy, balanced, or asset-light) based on tangible asset ratio.

**Step 5**: Synthesize using the **asset-based-valuation** prompt template and the **advanced-valuation-methodology** skill for adjustment factors and interpretation.

### Mode: `both` (Comps + Merton — legacy)

Execute both Comps and Merton workflows. Optimize by:
- Running `get_equity_snapshot_tool` once (shared by both)
- Running `run_equity_analysis_tool` once (shared by both)
- Running `compare_stocks_tool` for comps peers

Then produce a combined report with:
1. Comps section (following comparable-company-valuation prompt)
2. Merton section (following merton-model-valuation prompt)
3. **Synthesis section** comparing the two valuations:

```
## Valuation Synthesis

| Methodology | Implied Value | vs. Market Price |
|-------------|---------------|------------------|
| Comps (Weighted) | ${comps_val} | {+/-pct}% |
| Merton Model | ${merton_val} | {+/-pct}% |
| DCF (if available) | ${dcf_val} | {+/-pct}% |

**Consensus Range**: ${low} to ${high}
```

Reference the "Three-Pillar Valuation Framework" in the advanced-valuation-methodology skill if DCF data is also available.

### Mode: `all` (Comps + Merton + Asset-Based)

Execute all three workflows. Optimize by:
- Running `get_equity_snapshot_tool` once (shared by all)
- Running `run_equity_analysis_tool` once (shared by all)
- Running `compare_stocks_tool` for comps peers

Then produce a combined report with:
1. Comps section (following comparable-company-valuation prompt)
2. Merton section (following merton-model-valuation prompt)
3. Asset-Based section (following asset-based-valuation prompt)
4. **Synthesis section** comparing all valuations:

```
## Valuation Synthesis

| Methodology | Implied Value | vs. Market Price | Best For |
|-------------|---------------|------------------|----------|
| Comps (Weighted) | ${comps_val} | {+/-pct}% | Relative value vs. peers |
| Merton Model | ${merton_val} | {+/-pct}% | Leverage-adjusted value |
| Asset-Based (Adj. NAV) | ${nav_val} | {+/-pct}% | Floor value from assets |
| DCF (if available) | ${dcf_val} | {+/-pct}% | Intrinsic value from cash flows |

**Consensus Range**: ${low} to ${high}
**Weighted Consensus**: ${weighted_val} (using Four-Pillar weights)
```

Reference the "Four-Pillar Valuation Framework" in the advanced-valuation-methodology skill for weighting. Adjust weights based on the company's profile (asset-heavy, high-leverage, asset-light, etc.).

3. **Apply Agentman brand colors** per `references/brand-colors.md`, following the **agentman-pptx-style** design system: `AGENTMAN_100` (#F6EAE6) light fill table headers with `AGENTMAN_500` (#CC785C) terracotta text, `AGENTMAN_150` (#E3DACC) warm borders, charcoal text (#141413), `AGENTMAN_500` for undervalued/healthy emphasis, `AGENTMAN_600` (#A65945) for overvalued/high-risk emphasis, `CHARCOAL_950` bold for fair value, cream alternating rows (#FAF9F5), warm cream highlight rows (#F0EEE6). Green/red/amber/blue are **BANNED** (except ✓/✗ symbols).

4. **Deliver as a PDF or DOCX file** (user's choice, PDF by default). Use Python to generate a styled **PDF** (e.g., `reportlab`, `fpdf2`, `weasyprint`) or **DOCX** (e.g., `python-docx`) with Agentman brand colors, set document author to "Agentman Equity Research Assistant" and title to "Agentman — {Report Title}", save to the filesystem, and provide the file path. For DOCX, apply brand colors via `RGBColor` font colors, table cell shading, and custom styles per `references/brand-colors.md`. **NEVER deliver as HTML.** If an intermediate HTML step is needed, delete it after conversion.

5. End every report with the disclaimer:
   > *This research is for informational purposes only and does not constitute personalized investment advice. Past performance does not guarantee future results. Investors should conduct their own due diligence and consult a licensed financial advisor.*
