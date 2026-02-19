---
name: equity-research-planner
description: |
  Use when mapping out a research workflow. Provides query decomposition, tool selection matrices, plan templates, sequencing logic, and time estimation — so you know exactly what tools to use, in what order, and how long it will take.
---

This skill provides the methodology for creating structured equity research plans that are presented to users for approval before execution.

## Query Decomposition

### Step 1: Identify Research Parameters
- **Subject**: Which ticker(s) or sector(s)?
- **Depth**: Quick check, standard, or comprehensive?
- **Focus**: Valuation, comparison, news, financials, or all?
- **Constraints**: Specific time horizon, metrics, or concerns?

### Step 2: Map to Analysis Type

| Request Pattern | Analysis Type | Depth Level |
|----------------|---------------|-------------|
| "How is X doing?" | Quick Check | Quick |
| "What's happening with X?" | Standard + News | Standard |
| "Analyze X" / "Research X" | Standard | Standard |
| "Full report on X" / "Deep dive" | Comprehensive | Comprehensive |
| "Is X overvalued?" / "Fair value" | Valuation Focus | Standard-Comprehensive |
| "Compare X, Y, Z" | Comparison | Standard |
| "Best stock in [sector]" | Comparison + Valuation | Comprehensive |
| "Portfolio: X, Y, Z" | Portfolio Analysis | Standard |
| "Competitive landscape" / "SWOT" | Market Intelligence | Standard |

## Tool Selection Matrix

| Tool | Speed | Best For | Use When |
|------|-------|----------|----------|
| `get_equity_snapshot_tool` | ~10s | Quick metrics, P/E, ROE, ratings | Quick checks, supplementing other data |
| `run_market_analysis_tool` | ~30s | Profile, news, market context | News-focused queries, competitive analysis |
| `run_equity_analysis_tool` | ~45s | Comprehensive financials, ratios, history | Standard+ analysis, financial deep dives |
| `compare_stocks_tool` | ~30-60s | Side-by-side 2-5 stocks | Multi-stock queries, sector comparisons |
| `get_valuation_tool` | 1-3 min | DCF intrinsic value | Valuation questions, comprehensive reports |

## Sequencing Logic

### Parallelizable Combinations
These tool pairs can run simultaneously (no dependencies):
- `run_equity_analysis_tool` + `run_market_analysis_tool` (same ticker)
- `get_equity_snapshot_tool` + `get_valuation_tool` (same ticker)
- Multiple `get_equity_snapshot_tool` calls (different tickers)

### Sequential Dependencies
These should run in order:
- Context tools BEFORE `get_valuation_tool` (to interpret DCF results)
- `compare_stocks_tool` BEFORE individual deep-dives (to identify standouts)
- Data gathering BEFORE synthesis/reporting

## Time Estimation

| Depth | Typical Tools | Estimated Time |
|-------|---------------|----------------|
| Quick | 1 snapshot | ~15s |
| Standard | 2 tools in parallel | ~1-2 min |
| Comprehensive | 3-4 tools (some parallel) | ~4-6 min |
| Comparison (3 stocks) | compare + snapshots | ~1-2 min |
| Valuation Focus | snapshot + DCF | ~2-4 min |
| Full Report + Valuation | all tools | ~5-7 min |

## Plan Template

```
## Research Plan: [Topic]

**Scope**: [Quick Check / Standard Analysis / Comprehensive Report / Comparison / Valuation Focus / Market Intelligence]
**Estimated Time**: [total time accounting for parallelization]
**Ticker(s)**: [list]

| Step | Action | Tool | Purpose | Est. Time |
|------|--------|------|---------|-----------|
| 1 | ... | `tool_name` | ... | ~Xs |
| 2 | ... | `tool_name` | ... | ~Xs |
| 3 | Synthesize findings | - | Build report | ~30s |

**Parallelization**: Steps X and Y will run simultaneously, reducing total time.
**Deliverable**: [Quick summary / Structured report / Comparison table / Valuation assessment]

Shall I proceed with this plan?
```

## Example Plans

### Quick Check Plan
| Step | Action | Tool | Purpose | Est. Time |
|------|--------|------|---------|-----------|
| 1 | Get snapshot | `get_equity_snapshot_tool` | Key metrics, ratings | ~10s |
| 2 | Summarize | - | Present concise summary | ~10s |
**Total**: ~20s

### Standard Analysis Plan
| Step | Action | Tool | Purpose | Est. Time |
|------|--------|------|---------|-----------|
| 1 | Gather financials | `run_equity_analysis_tool` | Revenue, margins, ratios | ~45s |
| 2 | Gather market context | `run_market_analysis_tool` | Profile, news, ratings | ~30s |
| 3 | Synthesize | - | Build structured report | ~30s |
**Parallelization**: Steps 1 & 2 run simultaneously. **Total**: ~1.5 min

### Comprehensive Report Plan
| Step | Action | Tool | Purpose | Est. Time |
|------|--------|------|---------|-----------|
| 1 | Gather financials | `run_equity_analysis_tool` | Revenue, margins, ratios | ~45s |
| 2 | Gather market context | `run_market_analysis_tool` | Profile, news, ratings | ~30s |
| 3 | Run DCF valuation | `get_valuation_tool` | Intrinsic value estimate | ~2 min |
| 4 | Synthesize | - | Build comprehensive report | ~1 min |
**Parallelization**: Steps 1 & 2 run simultaneously. Step 3 after review. **Total**: ~4-5 min

## Brand Color & Styling

All deliverables planned by this skill MUST use the Agentman brand palette from `references/brand-colors.md`, following the **agentman-pptx-style** design system. When noting the deliverable format in research plans, assume brand colors are applied by default: `AGENTMAN_100` (#F6EAE6) light fill table headers with `AGENTMAN_500` (#CC785C) terracotta text, `AGENTMAN_150` (#E3DACC) warm borders, charcoal text (#141413), `AGENTMAN_500` for positive emphasis, `AGENTMAN_600` (#A65945) for negative emphasis, cream alternating rows (#FAF9F5). Green/red/amber/blue are **BANNED** (except ✓/✗ symbols).
