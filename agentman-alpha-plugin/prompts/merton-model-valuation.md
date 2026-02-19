---
name: merton-model-valuation
description: |
  Perform a Merton Model valuation treating equity as a European call option on firm assets.
  Use after collecting data from get_equity_snapshot_tool and run_equity_analysis_tool to extract
  market cap, total debt, beta, and shares outstanding. Produces a 7-section structural valuation report.
tools-required:
  - mcp__agentman-alpha__get_equity_snapshot_tool
  - mcp__agentman-alpha__run_equity_analysis_tool
estimated-time: 1-2 min
output-format: PDF or DOCX titled "Agentman — Merton Model Valuation", authored by "Agentman Equity Research Assistant"
---

# Merton Model Valuation

You are producing a structural equity valuation using the Merton Model (Black-Scholes framework). Equity is treated as a European call option on the firm's total assets, with debt as the strike price. You have collected data from:
1. **Equity Snapshot** — current price, market cap, shares outstanding, beta, key metrics
2. **Equity Analysis** — total debt, total equity, cash, financial ratios, balance sheet data

Reference the **advanced-valuation-methodology** skill for formulas, sensitivity parameters, and interpretation guidelines.

## Data Extraction Checklist

### From Equity Snapshot
- [ ] Current stock price
- [ ] Market capitalization
- [ ] Shares outstanding (compute: market cap / price if not directly available)
- [ ] Beta

### From Equity Analysis
- [ ] Total debt (short-term + long-term debt)
- [ ] Cash and cash equivalents
- [ ] Total stockholders' equity
- [ ] Debt-to-equity ratio (for validation)

### Derived Parameters
- [ ] Firm value V = Market Cap + Total Debt
- [ ] Strike price K = Total Debt
- [ ] Equity volatility sigma_E = Beta x 0.18
- [ ] Asset volatility sigma_V = sigma_E x (Market Cap / V)
- [ ] Risk-free rate r = 0.045 (4.5% 10-year Treasury proxy)
- [ ] Time to maturity T = 5 years (default)

## Computation Steps

### Step 1: Extract and Validate Inputs

Gather all parameters and perform sanity checks:
- Market Cap should be positive
- Total Debt should be positive (if zero or very small, note that Merton Model is uninformative for low-leverage companies)
- Beta should be between 0.2 and 3.0 (flag outliers)

Present inputs in a table before computing.

### Step 2: Compute Asset Volatility

```
sigma_E = Beta x 0.18
sigma_V = sigma_E x (Market Cap / (Market Cap + Total Debt))
```

Note: 0.18 is a proxy for annual S&P 500 market volatility. This is an approximation — actual equity volatility from options data would be more precise but is not available from current tools.

### Step 3: Compute d1 and d2

```
d1 = [ln(V / K) + (r + sigma_V^2 / 2) x T] / (sigma_V x sqrt(T))
d2 = d1 - sigma_V x sqrt(T)
```

Where:
- ln() is the natural logarithm
- V = Firm value (Market Cap + Total Debt)
- K = Total Debt
- r = 0.045
- T = 5
- sigma_V = asset volatility from Step 2

### Step 4: Compute Cumulative Normal Distribution Values

Use the approximation:
```
For x >= 0:
  k = 1 / (1 + 0.33267 x |x|)
  N(x) = 1 - n(x) x (0.4361836 x k + (-0.1201676) x k^2 + 0.9372980 x k^3)

For x < 0:
  N(x) = 1 - N(-x)

Where n(x) = (1 / sqrt(2 x pi)) x exp(-x^2 / 2)
```

Compute N(d1) and N(d2).

### Step 5: Compute Merton Equity Value

```
Equity Value = V x N(d1) - K x exp(-r x T) x N(d2)
Per-Share Value = Equity Value / Shares Outstanding
```

### Step 6: Compute Default Risk Metrics

```
Probability of Default = N(-d2) = 1 - N(d2)
Distance to Default = d2
```

### Step 7: Sensitivity Analysis

Re-run Steps 3-6 with parameter variations:

| Scenario | sigma_V | T | r |
|----------|---------|---|---|
| Base | computed | 5 | 4.5% |
| Low Vol / Short Maturity | sigma_V x 0.75 | 3 | 4.5% |
| Low Vol / Long Maturity | sigma_V x 0.75 | 7 | 4.5% |
| High Vol / Short Maturity | sigma_V x 1.25 | 3 | 4.5% |
| High Vol / Long Maturity | sigma_V x 1.25 | 7 | 4.5% |
| Low Rate | computed | 5 | 3.5% |
| High Rate | computed | 5 | 5.5% |

## Report Structure

### Header
```
# Agentman — Merton Model Valuation: {Company Name} ({TICKER})

**Date**: {date} | **Price**: ${price} | **Market Cap**: ${market_cap}
**Model**: Black-Scholes structural equity valuation
**Analyst**: Agentman Equity Research Assistant
```

### Section 1: Executive Summary (3-4 sentences)
- State the Merton Model implied equity value per share
- Compare to current market price (premium/discount percentage)
- State the implied probability of default and distance to default
- Note whether the model suggests the market is overpricing or underpricing default risk

### Section 2: Model Inputs
| Parameter | Symbol | Value | Source |
|-----------|--------|-------|--------|
| Market Capitalization | — | ${mkt_cap} | Equity snapshot |
| Total Debt | K | ${debt} | Equity analysis |
| Firm Value | V | ${firm_val} | Market Cap + Total Debt |
| Stock Beta | Beta | {beta} | Equity snapshot |
| Equity Volatility | sigma_E | {pct}% | Beta x 18% |
| Asset Volatility | sigma_V | {pct}% | sigma_E x (Mkt Cap / V) |
| Risk-Free Rate | r | 4.5% | 10Y Treasury proxy |
| Time to Maturity | T | 5 years | Default assumption |
| Shares Outstanding | N | {shares} | Equity snapshot |

Include a 1-2 sentence note on any input approximations or data limitations.

### Section 3: Black-Scholes Computation
Show the step-by-step calculation with actual numbers:

**Step 1**: d1 = [ln({V}/{K}) + (0.045 + {sigma_V}^2/2) x 5] / ({sigma_V} x sqrt(5)) = **{d1_value}**

**Step 2**: d2 = {d1_value} - {sigma_V} x sqrt(5) = **{d2_value}**

**Step 3**: N(d1) = **{Nd1}**, N(d2) = **{Nd2}**

**Step 4**: Equity Value = {V} x {Nd1} - {K} x exp(-0.045 x 5) x {Nd2} = **${equity_value}**

**Per-Share Value** = ${equity_value} / {shares} = **${per_share}**

### Section 4: Model vs. Market
| Metric | Value |
|--------|-------|
| Merton Equity Value (per share) | ${merton_value} |
| Current Market Price | ${current_price} |
| Premium / Discount | {pct}% |
| Implied Probability of Default | {pct}% |
| Distance to Default | {d2_value} |

#### Interpretation
Using the interpretation guidelines from the advanced-valuation-methodology skill:

| Metric | Value | Assessment |
|--------|-------|------------|
| Distance to Default | {d2} | {Healthy / Moderate Risk / High Risk} |
| Implied Default Prob | {pct}% | {Low / Moderate / High} |
| Merton / Market Price | {ratio}x | {In-line / Divergent} |

Provide 2-3 sentences explaining what the divergence (if any) between Merton value and market price implies about market pricing of default risk.

### Section 5: Sensitivity Analysis

#### Volatility x Maturity Matrix
| | T = 3 years | T = 5 years (base) | T = 7 years |
|---|---|---|---|
| **sigma_V x 0.75** | ${val} | ${val} | ${val} |
| **sigma_V (base)** | ${val} | **${base_val}** | ${val} |
| **sigma_V x 1.25** | ${val} | ${val} | ${val} |

#### Risk-Free Rate Sensitivity
| Rate | Per-Share Value | Default Prob |
|------|----------------|--------------|
| 3.5% | ${val} | {pct}% |
| 4.5% (base) | **${base_val}** | **{pct}%** |
| 5.5% | ${val} | {pct}% |

Note which parameter the model is most sensitive to and what that implies for confidence in the estimate.

### Section 6: Investment Implications
- 2-3 paragraphs interpreting the results in context
- Compare Merton value to current price and (if available) DCF value and comps-implied value
- Discuss what the distance to default and default probability mean for the investment case
- For low-leverage companies: note that the Merton value will be close to market cap (expected and uninformative)
- For high-leverage companies: discuss how changing interest rates or business performance could shift default risk

### Section 7: Key Risks & Caveats
- 3-5 bullets on methodology limitations:
  - Asset volatility is approximated from equity beta, not directly observed
  - Assumes log-normal asset returns (underestimates tail risk)
  - Single debt maturity assumption; real capital structures are more complex
  - Does not capture convertible debt, preferred equity, or off-balance-sheet obligations
  - Risk-free rate is a point-in-time assumption

### Disclaimer
> *This Agentman Merton Model valuation report is for informational purposes only and does not constitute personalized investment advice. The model involves significant simplifying assumptions about capital structure, volatility, and default dynamics. Past performance does not guarantee future results. Investors should conduct their own due diligence and consult a licensed financial advisor. Prepared by Agentman Equity Research Assistant.*

## Formatting Rules
- Use `$` for all currency values, `B` for billions
- Round all computed values to 4 decimal places in the computation section
- Round per-share values to 2 decimal places
- Round percentages to 2 decimal places
- Bold the final per-share value, distance to default, and default probability
- Present sensitivity tables with the base case bolded

## Brand Color Reference

All reports are output as **PDF or DOCX** (user's choice, PDF by default). Title: **"Agentman — Merton Model Valuation"** (set in document metadata and cover page). Author: **Agentman Equity Research Assistant** (display in header/cover and footer). For DOCX, use `python-docx` with brand colors applied via `RGBColor`, table cell shading, and custom styles. Apply the Agentman brand palette from `references/brand-colors.md`, following the **agentman-pptx-style** design system.

- **Visual weight**: 70% Carbon/Charcoal, 20% Warm Neutrals, 10% Terracotta accent
- **Section titles**: `CHARCOAL_900` (#292322) with `AGENTMAN_500` (#CC785C) underline
- **Body text**: `CHARCOAL_950` (#141413); secondary `SLATE_600` (#475569)
- **Table headers**: `AGENTMAN_100` (#F6EAE6) light fill, `AGENTMAN_500` (#CC785C) terracotta text
- **Table borders**: `AGENTMAN_150` (#E3DACC) warm
- **Alternating table rows**: `AGENTMAN_50` (#FAF9F5) cream / white
- **Distance to Default "Healthy"**: `AGENTMAN_500` (#CC785C) terracotta (positive)
- **Distance to Default "High Risk"**: `AGENTMAN_600` (#A65945) deep terracotta bold
- **Distance to Default "Moderate Risk"**: `CHARCOAL_950` (#141413) bold
- **Low default probability** (< 1%): `AGENTMAN_500` terracotta; **High default probability** (> 5%): `AGENTMAN_600` deep terracotta
- **Merton value vs. market** — underpriced risk: `AGENTMAN_600` deep terracotta; overpriced risk: `AGENTMAN_500` terracotta
- **Sensitivity table base case**: `AGENTMAN_75` (#F0EEE6) highlight row
- **Key per-share value**: `AGENTMAN_700` (#8B4A38) accent

**BANNED**: Green, red, amber, blue (except ✓/✗ comparison symbols). No gradients. No invented colors. See `references/color-antipatterns.md`.
