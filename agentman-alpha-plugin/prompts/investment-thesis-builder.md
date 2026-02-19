---
name: investment-thesis-builder
description: |
  Construct a structured investment thesis with bull and bear cases for a stock. Use after
  collecting comprehensive data from multiple tools. Produces a thesis document with catalysts,
  risks, valuation framework, and a clear conclusion structured for investment decision-making.
tools-required:
  - mcp__agentman-alpha__run_equity_analysis_tool
  - mcp__agentman-alpha__run_market_analysis_tool
  - mcp__agentman-alpha__get_valuation_tool (recommended)
  - mcp__agentman-alpha__get_equity_snapshot_tool (optional)
estimated-time: 4-6 min
output-format: PDF or DOCX titled "Agentman — Investment Thesis Builder", authored by "Agentman Equity Research Assistant"
---

# Investment Thesis Builder

You are constructing a structured investment thesis — the core document that articulates why an investor should or should not own a stock. This is the most opinionated output format: it takes a position (with caveats) rather than just presenting data.

## Thesis Construction Framework

### Step 1: Establish the Narrative
Every stock has a story. Identify the primary narrative:
- **Growth story**: Revenue accelerating, TAM expanding, new markets
- **Value story**: Cheap relative to earnings/cash flow, market overreacting to temporary headwinds
- **Turnaround story**: New management, restructuring, strategic pivot
- **Quality compounder**: Predictable growth, wide moat, capital return
- **Catalyst story**: Specific upcoming event that could unlock value
- **Income story**: High/growing dividend, stable cash flows

### Step 2: Test the Narrative Against Data
- Does the financial data support the narrative?
- What would have to be true for the thesis to work?
- What would invalidate the thesis?

## Report Structure

### Header
```
# Agentman — Investment Thesis: {Company Name} ({TICKER})

**Date**: {date} | **Price**: ${price} | **Market Cap**: ${mkt_cap}
**Analyst**: Agentman Equity Research Assistant

> **Thesis**: {One-sentence thesis statement — the core argument in 15-25 words}
```

### Section 1: Thesis Overview
3-4 paragraph narrative that tells the investment story:

**Paragraph 1 — The Setup**: What does the company do and why does it matter? What's the current market narrative?

**Paragraph 2 — The Opportunity**: What does the market misunderstand or underappreciate? What's the variant perception?

**Paragraph 3 — The Evidence**: What financial data supports the thesis? (cite specific numbers)

**Paragraph 4 — The Conclusion**: What needs to happen for the thesis to play out, and over what time horizon?

### Section 2: Bull Case

#### Core Arguments (5-7 bullets)
Each bullet follows this structure:
- **{Argument Label}**: {1-2 sentences with specific data}. *Evidence*: {metric or data point}.

Prioritize arguments by impact (most important first). Cover:
1. Revenue growth driver(s)
2. Margin expansion opportunity
3. Competitive moat / market position
4. Capital allocation (buybacks, dividends, M&A)
5. Valuation support (cheap relative to X)
6. Catalyst(s) (product launch, regulatory tailwind, cycle turn)
7. Management quality

#### Bull Case Price Target
"In the bull scenario, {TICKER} could trade at ${price} ({+pct}%), implying {X}x {metric} — achievable if {condition}."

### Section 3: Bear Case

#### Core Arguments (4-6 bullets)
Same structure as bull case. Cover:
1. Valuation risk (already priced for perfection)
2. Growth deceleration / revenue headwinds
3. Competitive threats
4. Margin pressure
5. Macro / regulatory / geopolitical risk
6. Execution risk

#### Bear Case Price Target
"In the bear scenario, {TICKER} could decline to ${price} ({-pct}%), which represents {X}x {metric} — a level consistent with {historical precedent or scenario}."

### Section 4: Valuation Framework

#### Current Valuation Context
| Metric | Value | vs. 5Y Avg (if known) | vs. Sector |
|--------|-------|-----------------------|------------|
| P/E | ... | ... | ... |
| P/S | ... | ... | ... |
| EV/EBITDA | ... | ... | ... |

#### DCF Assessment (if valuation tool was run)
| | |
|---|---|
| DCF Intrinsic Value | ${value} |
| Current Price | ${price} |
| Premium/Discount | {pct}% |
| Key Assumption Risk | {which input matters most} |

#### Comparable Company Analysis (Optional — include if comps data collected)
| Multiple | Target | Peer Median | Implied Value | Weight |
|----------|--------|-------------|---------------|--------|
| P/E | ... | ... | ${implied} | {w}% |
| EV/EBITDA | ... | ... | ${implied} | {w}% |
| P/S | ... | ... | ${implied} | {w}% |
| P/B | ... | ... | ${implied} | {w}% |
| **Weighted Fair Value** | — | — | **${fair_value}** | **100%** |

"Comps analysis using {N} peers ({peer list}) implies a fair value of ${fair_value}, suggesting the stock is trading at a {premium/discount} of {pct}% to peer-implied value."

#### Merton Model (Optional — include if Merton data collected)
| Metric | Value |
|--------|-------|
| Merton Equity Value (per share) | ${merton_val} |
| Distance to Default | {d2} |
| Implied Default Probability | {pct}% |
| Assessment | {Healthy / Moderate Risk / High Risk} |

"The Merton Model implies an equity value of ${merton_val} per share with a distance to default of {d2}, suggesting {interpretation of leverage risk}."

#### Valuation Synthesis (if multiple methodologies available)
| Methodology | Implied Value | vs. Current Price |
|-------------|---------------|-------------------|
| DCF | ${dcf_val} | {+/-pct}% |
| Comps | ${comps_val} | {+/-pct}% |
| Merton | ${merton_val} | {+/-pct}% |
| **Consensus** | **${consensus}** | **{+/-pct}%** |

#### Implied Expectations
"At ${current_price}, the market is pricing in approximately {X}% revenue growth and {Y}% operating margins over the next 5 years. This compares to the company's trailing {Z}% growth and {W}% margins."

### Section 5: Catalysts & Timeline

#### Near-Term Catalysts (0-6 months)
| Catalyst | Expected Timing | Impact | Probability |
|----------|----------------|--------|-------------|
| ... | ... | Positive/Negative | High/Med/Low |

#### Medium-Term Catalysts (6-18 months)
| Catalyst | Expected Timing | Impact | Probability |
|----------|----------------|--------|-------------|
| ... | ... | ... | ... |

### Section 6: What Would Change the Thesis

#### Thesis Invalidation Triggers (If these happen, reassess)
- "{Specific event or metric threshold}" — Would undermine the {bull/bear} case because...
- "{Specific event or metric threshold}" — ...

#### Thesis Confirmation Signals (If these happen, thesis is on track)
- "{Specific event or metric threshold}" — Would validate the {bull/bear} case because...
- "{Specific event or metric threshold}" — ...

### Section 7: Conclusion

#### Verdict
Present as one of:
- **Compelling Long**: Strong risk/reward favoring ownership
- **Attractive at Lower Levels**: Good company but valuation requires patience for better entry
- **Hold / Neutral**: Balanced risk/reward, better opportunities elsewhere
- **Proceed with Caution**: Risks outweigh potential rewards at current levels

#### Position Sizing Guidance (general, not personalized)
"Given the {risk profile}, this stock is appropriate as a {core/satellite/speculative} holding. The {volatility/concentration risk/binary catalyst} suggests position sizing of {modest/standard/conviction} weight."

#### Time Horizon
"This thesis has a {6-month / 12-month / 2-3 year} time horizon. The key milestone is {specific event/date}."

#### Investor Profile Suitability
Assess how the thesis maps to each investor profile:

| Profile | Suitability | Rationale |
|---------|-------------|-----------|
| **Conservative** | {Suitable / Partial / Not Suitable} | {1-sentence: Does the thesis offer capital preservation + income? Key factor: dividend, beta, margin of safety.} |
| **Moderate** | {Suitable / Partial / Not Suitable} | {1-sentence: Does the thesis offer balanced risk/reward? Key factor: PEG, analyst consensus, valuation.} |
| **Aggressive** | {Suitable / Partial / Not Suitable} | {1-sentence: Does the thesis offer high upside? Key factor: growth rate, catalysts, momentum.} |

"This thesis is best suited for **{profile}** investors because {1-sentence connecting the thesis narrative to the profile's priorities}."

### Disclaimer
> *This Agentman investment thesis is for informational purposes only and does not constitute personalized investment advice. The bull and bear cases represent possible scenarios, not predictions. Past performance does not guarantee future results. Investors should conduct their own due diligence and consult a licensed financial advisor. Prepared by Agentman Equity Research Assistant.*

## Thesis Quality Checklist
Before finalizing, verify:
- [ ] Thesis statement is clear, specific, and falsifiable
- [ ] Bull and bear cases are balanced (not just cheerleading or doom-saying)
- [ ] Every argument is supported by specific data, not vague assertions
- [ ] Valuation is grounded in numbers, not feelings
- [ ] Invalidation triggers are specific enough to be actionable
- [ ] Time horizon is explicit
- [ ] The conclusion follows logically from the evidence presented

## Brand Color Reference

All reports are output as **PDF or DOCX** (user's choice, PDF by default). Title: **"Agentman — Investment Thesis Builder"** (set in document metadata and cover page). Author: **Agentman Equity Research Assistant** (display in header/cover and footer). For DOCX, use `python-docx` with brand colors applied via `RGBColor`, table cell shading, and custom styles. Apply the Agentman brand palette from `references/brand-colors.md`, following the **agentman-pptx-style** design system.

- **Visual weight**: 70% Carbon/Charcoal, 20% Warm Neutrals, 10% Terracotta accent
- **Section titles**: `CHARCOAL_900` (#292322) with `AGENTMAN_500` (#CC785C) underline
- **Body text**: `CHARCOAL_950` (#141413); secondary `SLATE_600` (#475569)
- **Table headers**: `AGENTMAN_100` (#F6EAE6) light fill, `AGENTMAN_500` (#CC785C) terracotta text
- **Table borders**: `AGENTMAN_150` (#E3DACC) warm
- **Alternating table rows**: `AGENTMAN_50` (#FAF9F5) cream / white
- **Bull case elements** (positive catalysts, upside): `AGENTMAN_500` (#CC785C) terracotta
- **Bear case elements** (risks, downside): `AGENTMAN_600` (#A65945) deep terracotta
- **Mixed/neutral signals**: `CHARCOAL_950` (#141413) bold
- **Verdict boxes**: `AGENTMAN_500` (#CC785C) border + `AGENTMAN_50` (#FAF9F5) cream bg for ALL verdicts (same box style regardless of verdict)
- **Catalyst impact column**: Positive = `AGENTMAN_500` terracotta, Negative = `AGENTMAN_600` deep terracotta, Mixed = `CHARCOAL_950` bold
- **Terracotta budget**: max 3 `AGENTMAN_500` elements per section

**BANNED**: Green, red, amber, blue (except ✓/✗ comparison symbols). No gradients. No invented colors. See `references/color-antipatterns.md`.
