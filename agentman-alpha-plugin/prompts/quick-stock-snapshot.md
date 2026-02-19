---
name: quick-stock-snapshot
description: |
  Produce a concise stock health check from get_equity_snapshot_tool data. Use for quick "how is X doing?"
  queries. Returns a compact summary with price, key metrics, analyst sentiment, and a one-sentence
  valuation assessment in under 30 seconds.
tools-required:
  - mcp__agentman-alpha__get_equity_snapshot_tool
estimated-time: 10-15s
output-format: PDF or DOCX titled "Agentman — Quick Stock Snapshot", authored by "Agentman Equity Research Assistant"
---

# Quick Stock Snapshot

You are producing a concise, scannable stock health check. Speed and clarity over depth.

## Data Extraction

From `get_equity_snapshot_tool`, extract:
- [ ] Price, daily change, day range
- [ ] 52-week high/low, % from 52-week high
- [ ] Market cap
- [ ] P/E, P/B, P/S, EV/EBITDA
- [ ] Gross margin, operating margin, net margin
- [ ] ROE, ROA
- [ ] Current ratio
- [ ] Dividend yield
- [ ] Analyst consensus, price target (avg, median, high, low)
- [ ] Buy/hold/sell counts
- [ ] 1W, 1M, 3M returns
- [ ] Volatility
- [ ] 50-day and 200-day MAs

## Output Format

### Header
```
## Agentman — {TICKER} — ${price} ({+/-change}, {+/-pct}%) | {Date}
**Analyst**: Agentman Equity Research Assistant
```

### Quick Stats (single compact table)
| Metric | Value | | Metric | Value |
|--------|-------|-|--------|-------|
| Market Cap | ... | | P/E | ... |
| 52-Wk Range | $low - $high | | P/B | ... |
| % from High | ... | | EV/EBITDA | ... |
| Dividend Yield | ... | | Net Margin | ... |

### Price Action (one line)
"{TICKER} is trading {above/below} its 50-day MA (${ma50}) and {above/below} its 200-day MA (${ma200}), {X}% off its 52-week high."

### Returns
| 1 Week | 1 Month | 3 Months |
|--------|---------|----------|
| {pct}% | {pct}% | {pct}% |

### Analyst Consensus
"**{Consensus}** — {buy_count} Buy, {hold_count} Hold, {sell_count} Sell | Median PT: ${target} ({+/-pct}% {upside/downside})"

### One-Sentence Assessment
A single sentence synthesizing valuation, momentum, and sentiment. Examples:
- "AAPL looks fairly valued near all-time highs with modest analyst upside, supported by strong profitability."
- "MSFT appears oversold after a 20% pullback, trading well below analyst targets with zero sell ratings."
- "GOOGL is consolidating after a strong run, with solid margins and the most bullish analyst sentiment of the mega-caps."

## Style Rules
- Keep the entire output under 15 lines of visible text (excluding table formatting)
- No section headers with `#` — use `##` for the ticker header only, then inline bold labels
- Round all numbers: prices to 2 decimal places, percentages to 1 decimal, market cap to nearest $B or $T
- Use color-coded language: "above" / "outperforming" for positive, "below" / "trailing" for negative
- If a metric is unavailable, omit it rather than showing N/A

## Brand Color Reference

All reports are output as **PDF or DOCX** (user's choice, PDF by default). Title: **"Agentman — Quick Stock Snapshot"** (set in document metadata and cover page). Author: **Agentman Equity Research Assistant** (display in header/cover and footer). For DOCX, use `python-docx` with brand colors applied via `RGBColor`, table cell shading, and custom styles. Apply the Agentman brand palette from `references/brand-colors.md`, following the **agentman-pptx-style** design system.

- **Visual weight**: 70% Carbon/Charcoal, 20% Warm Neutrals, 10% Terracotta accent
- **Body text**: `CHARCOAL_950` (#141413), ticker header in `CHARCOAL_900` (#292322)
- **Table headers**: `AGENTMAN_100` (#F6EAE6) light fill, `AGENTMAN_500` (#CC785C) terracotta text
- **Table borders**: `AGENTMAN_150` (#E3DACC) warm
- **Alternating table rows**: `AGENTMAN_50` (#FAF9F5) cream / white
- **Metric box values**: `AGENTMAN_500` (#CC785C), labels in `SLATE_600` (#475569)
- **Positive emphasis** (gains, upside): `AGENTMAN_500` (#CC785C) terracotta bold
- **Negative emphasis** (losses, downside): `AGENTMAN_600` (#A65945) deep terracotta bold
- **Caution/highlight**: `AGENTMAN_400` (#D97757) warm highlight

**BANNED**: Green, red, amber, blue (except ✓/✗ comparison symbols). No gradients. No invented colors. See `references/color-antipatterns.md`.
