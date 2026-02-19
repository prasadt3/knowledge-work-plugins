# agentman-alpha Equity Research Plugin v2.3

Get institutional-quality equity research — comprehensive reports, DCF valuations, peer comparisons, and investor profile scoring — directly in Claude Code. A structured, **planning-first workflow** puts you in control: review and approve the research plan before any data is collected. Supports **four valuation methodologies** (Damodaran DCF, Comparable Company Analysis, Merton Model, Asset-Based NAV) and **investor profile scoring** across Conservative, Moderate, and Aggressive lenses.

## Architecture

### 7-Agent Hierarchy

```
User Query
  │
  ├─ /research ────────────► Orchestrator (plans + executes)
  │                            ├─► Financial Data Specialist
  │                            ├─► Market Analyst Pro
  │                            ├─► Stock Analysis Specialist
  │                            ├─► Market Intelligence Analyst
  │                            └─► Investor Profile Analyst
  │
  ├─ /stock-check ─────────► Quick snapshot (direct)
  ├─ /stock-analysis ──────► Full report (direct)
  ├─ /stock-compare ───────► Comparison (direct)
  ├─ /stock-valuation ─────► DCF valuation (direct)
  ├─ /market-research ─────► Competitive intelligence (direct)
  ├─ /investor-valuation ──► Profile scoring (direct)
  └─ /advanced-valuation ─► Comps + Merton Model (direct)
```

| Agent | Model | Role | Tools |
|-------|-------|------|-------|
| **equity-research-orchestrator** | opus | Routes requests, coordinates specialists, synthesizes reports | All 5 |
| **equity-research-planner** | opus | Creates structured research plans (no data fetching) | None |
| **financial-data-specialist** | sonnet | Real-time data, portfolio analysis, earnings tracking | `get_equity_snapshot_tool`, `run_equity_analysis_tool` |
| **market-analyst-pro** | sonnet | Multi-stock comparisons, sector trends | `compare_stocks_tool` |
| **stock-analysis-specialist** | sonnet | DCF, comps, Merton model, asset-based NAV, fundamental/technical/sentiment | `get_valuation_tool`, `get_equity_snapshot_tool`, `compare_stocks_tool`, `run_equity_analysis_tool` |
| **market-intelligence-analyst** | sonnet | Competitive intelligence, SWOT, Porter's Five Forces | `run_market_analysis_tool` |
| **investor-profile-analyst** | sonnet | Profile-based scoring (Conservative/Moderate/Aggressive) | `get_equity_snapshot_tool`, `run_equity_analysis_tool`, `get_valuation_tool` |

### Planning-First Workflow

The `/research` command uses a two-phase approach:

**Phase 1 - Plan:** Analyze the user's query, create a structured Research Plan with a table of steps, tools, purposes, and time estimates. Present the plan and **wait for approval**.

**Phase 2 - Execute:** After approval, run tools in the planned order (parallelizing where possible), synthesize into the appropriate report format, and add disclaimers.

```
User: /research AAPL

Phase 1 → Research Plan presented:
  Step 1: Gather financials (run_equity_analysis_tool, ~45s)
  Step 2: Gather market context (run_market_analysis_tool, ~30s)  [parallel with Step 1]
  Step 3: Run DCF valuation (get_valuation_tool, ~2min)
  "Shall I proceed?"

Phase 2 → User approves → Tools execute → Structured report delivered
```

## Installation

1. Clone or copy the `agentman-alpha-plugin/` directory
2. Install dependencies:
   ```bash
   cd /path/to/agentman-alpha-mcp-server
   uv sync
   ```
3. Create a `.env` file with at minimum:
   ```
   FINANCIALMODELINGPREP_API_KEY=your_key_here
   ```
4. For DCF valuation, also add:
   ```
   GOOGLE_CREDENTIALS_JSON=your_credentials
   ```
5. Configure the plugin in your Claude Code project settings (`.claude/settings.json`):
   ```json
   {
     "plugins": ["./agentman-alpha-plugin"]
   }
   ```

## Commands

| Command | Description | Example |
|---|---|---|
| `/research <TICKER>` | Comprehensive planned research workflow | `/research AAPL` |
| `/market-research <TICKER>` | Competitive intelligence and SWOT analysis | `/market-research GOOGL` |
| `/stock-check <TICKER>` | Quick snapshot with key metrics | `/stock-check AAPL` |
| `/stock-analysis <TICKER>` | Full research report (direct, no planning phase) | `/stock-analysis NVDA` |
| `/stock-compare <TICKERS>` | Side-by-side comparison of 2-5 stocks | `/stock-compare AAPL,MSFT,GOOGL` |
| `/stock-valuation <TICKER>` | Damodaran DCF intrinsic value estimate | `/stock-valuation TSLA` |
| `/investor-valuation <TICKER> [profile]` | Score stock for Conservative/Moderate/Aggressive profiles | `/investor-valuation AAPL conservative` |
| `/advanced-valuation <TICKER> [comps\|merton\|asset\|both\|all]` | Comparable Company Analysis, Merton Model, and/or Asset-Based Valuation | `/advanced-valuation NVDA comps` |

### Quick vs. Planned Workflows

- **Quick commands** (`/stock-check`, `/stock-analysis`, `/stock-compare`, `/stock-valuation`, `/market-research`, `/investor-valuation`, `/advanced-valuation`): Execute immediately without a planning phase. Best for focused, single-purpose queries.
- **Planned commands** (`/research`): Creates a research plan first, presents it for approval, then executes. Best for comprehensive, multi-dimensional analysis.
- **Profile-aware commands**: `/investor-valuation` scores a stock across all three profiles. `/research` detects profile keywords (e.g., "conservative analysis AAPL") and adds profile scoring to the output.
- **Multi-method valuation**: `/advanced-valuation` supports `comps`, `merton`, `asset`, `both` (comps + merton), and `all` (comps + merton + asset) modes for comprehensive valuation from multiple angles.

## Skills

| Skill | Purpose |
|-------|---------|
| **equity-research-assistant** | Orchestration: routing logic, report templates, compliance guardrails |
| **equity-research-planner** | Planning: query decomposition, tool selection, sequencing, time estimation |
| **financial-data-specialist** | Data frameworks: portfolio analysis, earnings tracking, metrics interpretation |
| **market-analyst-pro** | Market frameworks: sector analysis, comparative analysis, trend identification |
| **stock-analysis-specialist** | Analysis frameworks: fundamental/technical/sentiment, DCF context, risk assessment |
| **investor-profile-methodology** | Investor profile scoring: rubrics, thresholds, interpretation for Conservative/Moderate/Aggressive profiles |
| **advanced-valuation-methodology** | Advanced valuation frameworks: Comparable Company Analysis (comps) formulas, Merton Model (Black-Scholes), Asset-Based Valuation (NAV), weighting schemes, peer selection, interpretation |

## Tools (via MCP Server)

| Tool | Speed | Use Case |
|---|---|---|
| `get_equity_snapshot_tool` | ~10s | Quick health check: P/E, ROE, analyst ratings |
| `run_market_analysis_tool` | ~30s | Market data + company profile + news |
| `run_equity_analysis_tool` | ~45s | Comprehensive financials + price history |
| `compare_stocks_tool` | ~30-60s | Side-by-side comparison of 2-5 stocks |
| `get_valuation_tool` | 1-3 min | Damodaran DCF intrinsic value estimate |

## Example Workflows

### Quick Stock Check
```
/stock-check AAPL
→ Instant snapshot with key metrics and one-sentence assessment
```

### Full Planned Research
```
/research AAPL
→ Phase 1: Research plan presented for approval
→ Phase 2: Execute plan, synthesize comprehensive report
```

### Stock Comparison
```
/research Compare AMD INTC NVDA
→ Plan: compare_stocks_tool + individual snapshots
→ Side-by-side table with relative value analysis
```

### Competitive Intelligence
```
/market-research GOOGL
→ SWOT analysis, competitive positioning, industry dynamics
```

### Investor Profile Analysis
```
/investor-valuation AAPL
→ Scores AAPL for Conservative (50pts), Moderate (50pts), Aggressive (50pts)
→ Determines best-fit profile with action guidance
```

### Profile-Aware Research
```
/research conservative analysis AAPL
→ Detects "conservative" keyword → adds profile scoring to comprehensive report
```

### Comparable Company Analysis
```
/advanced-valuation NVDA comps
→ Identifies 3-5 semiconductor peers, compares multiples
→ Computes weighted fair value from peer median P/E, EV/EBITDA, P/S, P/B
```

### Merton Model (Default Risk)
```
/advanced-valuation TSLA merton
→ Treats equity as call option on firm assets
→ Computes Black-Scholes value, distance to default, implied default probability
```

### Asset-Based Valuation (NAV)
```
/advanced-valuation JPM asset
→ Computes Book Value, Tangible Book Value, Net-Net Working Capital, Adjusted NAV
→ Classifies asset profile and applies fair-value adjustments
```

### Full Advanced Valuation
```
/advanced-valuation AAPL all
→ Runs Comps, Merton Model, and Asset-Based Valuation
→ Produces synthesis table comparing all methodologies using Four-Pillar weights
```

### Legacy Combined Valuation
```
/advanced-valuation AAPL both
→ Runs Comps and Merton Model (legacy mode)
→ Produces synthesis table comparing both methodologies (+ DCF if available)
```

### Portfolio Analysis
```
"Analyze my portfolio AAPL MSFT GOOGL"
→ Financial data specialist: snapshots + comparison + synthesis
```

## Investor Profiles

The plugin evaluates stocks through three distinct investor lenses, each with its own 50-point scoring rubric:

| Profile | Focus | Key Criteria | DCF Tolerance |
|---------|-------|-------------|---------------|
| **Conservative** | Capital preservation, income | Dividends, balance sheet, earnings stability, margin of safety, low beta | <= 1.1x intrinsic value |
| **Moderate** | Balanced growth + income | PEG ratio, profitability, analyst consensus, reasonable valuation, risk-adjusted returns | Up to ~1.5x |
| **Aggressive** | Capital appreciation | Revenue growth, TAM, momentum, disruption potential, upside targets | 2-3x+ for high growth |

**Score Interpretation**: 40-50 = Excellent Fit, 30-39 = Good Fit, 20-29 = Moderate Fit, 10-19 = Poor Fit, 0-9 = Not Suitable

Profile scoring is available via `/investor-valuation` and is integrated into comprehensive reports, comparisons, valuations, risk assessments, thesis builders, and portfolio reviews.

## Brand Color System

All reports are output as **PDF or DOCX** (user's choice, PDF by default), titled **"Agentman — {Report Title}"** and authored by **Agentman Equity Research Assistant**, following the **agentman-pptx-style** design system. For DOCX output, use `python-docx` with the same Agentman brand colors applied via custom styles, table shading, and font colors. The brand identity is **quiet confidence** — charcoal suits, not fire trucks.

| Element | Color | Hex |
|---------|-------|-----|
| Table headers | Light fill + terracotta text | #F6EAE6 bg, #CC785C text |
| Table borders | Warm neutral | #E3DACC |
| Section title underline | Terracotta accent | #CC785C |
| Body text | Charcoal | #141413 |
| Alternating table rows | Light cream / white | #FAF9F5 |
| Highlight rows (totals) | Warm cream | #F0EEE6 |
| Positive emphasis | Terracotta | #CC785C |
| Negative emphasis | Deep terracotta | #A65945 |

**Visual weight**: 70% Carbon/Charcoal, 20% Warm Neutrals, 10% Terracotta accent. Green, red, amber, and blue are **banned** from reports (except ✓/✗ comparison symbols). No gradients. See `references/brand-colors.md` for the complete palette and `references/color-antipatterns.md` for forbidden patterns.

## Requirements

- Python 3.10+
- `FINANCIALMODELINGPREP_API_KEY` (required for all tools)
- `GOOGLE_CREDENTIALS_JSON` or `GOOGLE_CREDENTIALS_BASE64` (required for valuation tool)
- Claude Code CLI installed
