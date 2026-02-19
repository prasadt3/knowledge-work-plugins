---
name: prompts-directory
description: Synthesis prompt templates for the agentman-alpha equity research plugin
---

# Prompts

This directory contains **synthesis prompt templates** — detailed instructions for how to process, analyze, and present equity research data after it has been collected from MCP tools.

## How Prompts Fit in the Plugin Architecture

```
commands/     → What the user triggers (slash commands)
agents/       → Who does the work (agent personas with tool access)
skills/       → How to think about the work (methodology frameworks)
prompts/      → How to present the work (synthesis & output templates)
```

Prompts are the detailed blueprints that guide the AI through:
1. **Data extraction** — What to pull from raw tool output
2. **Computation** — What derived metrics to calculate (e.g., P/E from price/EPS, YoY growth rates)
3. **Report structure** — Exact sections, tables, and narrative format
4. **Interpretation guidelines** — How to contextualize numbers and avoid common pitfalls
5. **Quality standards** — Formatting rules, required disclaimers, and analysis rigor

## Available Prompts

| Prompt | Use Case | Tools Required | Est. Time |
|--------|----------|----------------|-----------|
| [comprehensive-equity-report](comprehensive-equity-report.md) | Full research report on a single stock | equity + market + valuation | 4-6 min |
| [stock-comparison](stock-comparison.md) | Side-by-side comparison of 2-5 stocks | compare + snapshots | 1-2 min |
| [dcf-valuation-analysis](dcf-valuation-analysis.md) | Intrinsic value assessment with caveats | valuation + snapshot | 2-4 min |
| [quick-stock-snapshot](quick-stock-snapshot.md) | Fast stock health check | snapshot | 10-15s |
| [market-intelligence-swot](market-intelligence-swot.md) | SWOT, Porter's Five Forces, competitive positioning | market + compare | 1-2 min |
| [earnings-analysis](earnings-analysis.md) | Quarterly/annual earnings review | equity + market | 1-2 min |
| [sector-analysis](sector-analysis.md) | Sector-level landscape with rankings | compare + market | 1-3 min |
| [portfolio-review](portfolio-review.md) | Multi-holding portfolio assessment | compare + snapshots | 1-3 min |
| [risk-assessment](risk-assessment.md) | Focused risk profile with scenarios | equity + snapshot | 1-2 min |
| [investment-thesis-builder](investment-thesis-builder.md) | Bull/bear thesis construction | all tools | 4-6 min |
| [investor-profile-valuation](investor-profile-valuation.md) | Score stock across Conservative/Moderate/Aggressive profiles | snapshot + equity + valuation | 3-5 min |
| [comparable-company-valuation](comparable-company-valuation.md) | Relative valuation via peer multiples (P/E, EV/EBITDA, P/S, P/B) | compare + snapshot + equity | 1-3 min |
| [merton-model-valuation](merton-model-valuation.md) | Structural equity valuation (Black-Scholes framework) with default risk | snapshot + equity | 1-2 min |
| [asset-based-valuation](asset-based-valuation.md) | Net asset value from balance sheet (Book Value, Tangible BV, Adjusted NAV) | equity + snapshot | 1-2 min |

## Brand Color System

All prompts reference the Agentman brand color palette defined in `references/brand-colors.md`, following the **agentman-pptx-style** design system. The brand identity is **quiet confidence** — charcoal suits, not fire trucks. Each prompt includes a **Brand Color Reference** section mapping colors to report elements:

- **Visual weight**: 70% Carbon/Charcoal, 20% Warm Neutrals, 10% Terracotta accent
- **Table headers**: `AGENTMAN_100` (#F6EAE6) light fill + `AGENTMAN_500` (#CC785C) terracotta text
- **Table borders**: `AGENTMAN_150` (#E3DACC) warm borders
- **Text hierarchy**: charcoal for body/headings, slate for secondary/meta text
- **Emphasis**: Terracotta family (`AGENTMAN_500` positive, `AGENTMAN_600` negative, `AGENTMAN_400` highlight)
- **Banned colors**: Green, red, amber, blue banned from reports (except ✓/✗ comparison symbols). No gradients.
- **Terracotta budget**: Max 3 `AGENTMAN_500` elements per section

All reports are output as **PDF or DOCX** (user's choice, PDF by default), titled **"Agentman — {Report Title}"** and authored by **Agentman Equity Research Assistant**. For DOCX output, use `python-docx` with the same brand colors applied via `RGBColor`, table cell shading, and custom styles. See `references/color-antipatterns.md` for forbidden patterns and the brand-colors reference for hex values.

## Prompt Structure

Each prompt follows a consistent format:

```markdown
---
name: prompt-name
description: What this prompt does and when to use it
tools-required: Which MCP tools feed data into this prompt
estimated-time: How long the full workflow takes
output-format: What the final output looks like
---

# Title

## Data Extraction Checklist
What to pull from raw tool output before writing.

## Report Structure
Section-by-section template with tables, narrative guidance, and examples.

## Analysis/Formatting Guidelines
Rules for interpretation, formatting, and quality.
```

## Mapping: Commands → Prompts

| Command | Primary Prompt | Fallback Prompt |
|---------|---------------|-----------------|
| `/research` (comprehensive) | comprehensive-equity-report | — |
| `/research` (quick) | quick-stock-snapshot | — |
| `/research` (comparison) | stock-comparison | — |
| `/research` (valuation) | dcf-valuation-analysis | — |
| `/research` (SWOT) | market-intelligence-swot | — |
| `/stock-check` | quick-stock-snapshot | — |
| `/stock-analysis` | comprehensive-equity-report | — |
| `/stock-compare` | stock-comparison | — |
| `/stock-valuation` | dcf-valuation-analysis | — |
| `/market-research` | market-intelligence-swot | sector-analysis |
| `/investor-valuation` | investor-profile-valuation | — |
| `/research` (profile) | investor-profile-valuation | — |
| `/advanced-valuation` (comps) | comparable-company-valuation | — |
| `/advanced-valuation` (merton) | merton-model-valuation | — |
| `/advanced-valuation` (asset) | asset-based-valuation | — |
| `/advanced-valuation` (both) | comparable-company-valuation + merton-model-valuation | — |
| `/advanced-valuation` (all) | comparable-company-valuation + merton-model-valuation + asset-based-valuation | — |
| `/research` (comps) | comparable-company-valuation | — |
| `/research` (merton) | merton-model-valuation | — |
| `/research` (asset/NAV) | asset-based-valuation | — |

## Combining Prompts

For complex workflows, prompts can be chained:

- **Full research report**: comprehensive-equity-report + risk-assessment
- **Investment decision**: investment-thesis-builder (uses data from all other prompts)
- **Portfolio rebalancing**: portfolio-review + sector-analysis
- **Earnings reaction**: earnings-analysis + quick-stock-snapshot (for current positioning)
- **Deep competitive study**: market-intelligence-swot + stock-comparison + sector-analysis
- **Profile-aware research**: investor-profile-valuation + comprehensive-equity-report
- **Profile-aware comparison**: stock-comparison (includes Section 9: Investor Profile Fit)
- **Advanced valuation**: comparable-company-valuation + merton-model-valuation + asset-based-valuation
- **Full multi-method valuation**: dcf-valuation-analysis + comparable-company-valuation + merton-model-valuation + asset-based-valuation
