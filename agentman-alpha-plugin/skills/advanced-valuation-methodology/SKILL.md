---
name: advanced-valuation-methodology
description: |
  Use when you need valuation beyond DCF — peer comparisons via Comps, leverage-adjusted value
  via the Merton Model, or floor value from balance sheet assets (NAV). Provides formulas,
  weighting schemes, and interpretation guidelines for all three methodologies.
---

This skill provides three advanced valuation methodologies that complement the existing Damodaran DCF approach. All methodologies compute values using data already available from existing MCP tools — no additional backend is required.

## Methodology 1: Comparable Company Analysis (Comps)

### Purpose
Value a stock by comparing its trading multiples to a peer group of 3-5 similar companies, deriving an implied fair value range.

### Peer Selection Criteria

Select 3-5 peers based on these factors (in priority order):
1. **Same sub-industry** (e.g., semiconductor fabless, SaaS infrastructure)
2. **Similar market cap range** (within 0.3x to 3x of target)
3. **Similar revenue scale** (within 0.5x to 2x)
4. **Similar growth profile** (revenue growth within 10 percentage points)
5. **Similar margin profile** (operating margin within 10 percentage points)

If fewer than 3 strong matches exist, relax criteria 2-5 in order.

### Multiples Used

| Multiple | Formula | Best For |
|----------|---------|----------|
| P/E (TTM) | Price / TTM EPS | Profitable, stable-earnings companies |
| EV/EBITDA | Enterprise Value / TTM EBITDA | Capital-intensive, leveraged companies |
| P/S (TTM) | Price / (TTM Revenue / Shares) | High-growth, pre-profit companies |
| P/B | Price / Book Value per Share | Asset-heavy companies (banks, REITs) |

### Default Weighting Scheme

| Multiple | Default Weight | Rationale |
|----------|---------------|-----------|
| P/E | 35% | Most widely used, directly ties to earnings |
| EV/EBITDA | 30% | Capital-structure neutral, good cross-company |
| P/S | 20% | Useful when earnings volatile |
| P/B | 15% | Floor valuation, asset-based |

### Weight Adjustments

| Condition | Adjustment |
|-----------|------------|
| Target has negative EPS | P/E weight → 0%. Redistribute: EV/EBITDA 40%, P/S 30%, P/B 30% |
| Target has negative EBITDA | EV/EBITDA weight → 0%. Redistribute: P/E 50%, P/S 30%, P/B 20% |
| Both EPS and EBITDA negative | P/S 60%, P/B 40% |
| Target is a bank/REIT | P/B 40%, P/E 35%, P/S 15%, EV/EBITDA 10% |

### Implied Value Computation

**Per-multiple implied values:**
- **P/E implied**: `Peer Median P/E x Target TTM EPS`
- **P/S implied**: `Peer Median P/S x (Target TTM Revenue / Shares Outstanding)`
- **P/B implied**: `Peer Median P/B x Target Book Value per Share`
- **EV/EBITDA implied**: `(Peer Median EV/EBITDA x Target TTM EBITDA - Net Debt) / Shares Outstanding`

**Weighted fair value:**
```
Fair Value = Sum(Weight_i x Implied Value_i) for each applicable multiple
```

**Fair value range:**
- **Low bound**: Use 25th percentile peer multiples instead of median
- **High bound**: Use 75th percentile peer multiples instead of median

### Premium/Discount Justification

After computing the comps-implied value, assess whether the target deserves a premium or discount vs. peers:

| Factor | Premium Warranted | Discount Warranted |
|--------|------------------|--------------------|
| Growth | Faster than peer median | Slower than peer median |
| Margins | Higher and expanding | Lower or compressing |
| Market position | #1-2 in market | Lagging competitor |
| Balance sheet | Net cash, low leverage | High debt, tight liquidity |
| Analyst sentiment | Mostly Buy/Strong Buy | Mostly Hold/Sell |

Typical adjustment range: -15% to +20% from comps-implied value.

## Methodology 2: Merton Model (Structural Credit Model)

### Purpose
Treat equity as a European call option on the firm's total assets, with debt as the strike price. This provides an alternative equity valuation that explicitly accounts for leverage and default risk. Particularly useful for assessing highly leveraged companies or comparing the market's implied default probability to fundamentals.

### Parameter Extraction from Existing Tools

| Parameter | Symbol | Source | Computation |
|-----------|--------|--------|-------------|
| Firm value | V | snapshot + equity analysis | Market Cap + Total Debt (book value) |
| Strike price | K | equity analysis | Total Debt (book value) |
| Time to maturity | T | assumption | 5 years (default, weighted-avg debt maturity) |
| Equity volatility | sigma_E | equity analysis | Beta x 0.18 (market vol proxy) |
| Asset volatility | sigma_V | derived | sigma_E x (Market Cap / V) |
| Risk-free rate | r | assumption | 4.5% (10-year Treasury proxy) |
| Shares outstanding | N | snapshot | Shares outstanding from quote data |

### Black-Scholes Computation

**Step 1: Compute d1 and d2**
```
d1 = [ln(V/K) + (r + sigma_V^2 / 2) * T] / (sigma_V * sqrt(T))
d2 = d1 - sigma_V * sqrt(T)
```

**Step 2: Compute N(d1) and N(d2)**
Use the cumulative normal distribution function. Approximation for N(x):
```
If x >= 0:  N(x) = 1 - n(x) * (a1*k + a2*k^2 + a3*k^3)
If x < 0:   N(x) = 1 - N(-x)

Where:
  k = 1 / (1 + 0.33267 * |x|)
  a1 = 0.4361836, a2 = -0.1201676, a3 = 0.9372980
  n(x) = (1/sqrt(2*pi)) * exp(-x^2/2)    [standard normal PDF]
```

**Step 3: Compute equity value**
```
Equity Value = V * N(d1) - K * exp(-r * T) * N(d2)
Per-Share Value = Equity Value / Shares Outstanding
```

**Step 4: Implied default probability**
```
Probability of Default = N(-d2)
Distance to Default = d2
```

### Sensitivity Analysis Parameters

Run the model with these variations to show sensitivity:

| Parameter | Base | Low | High |
|-----------|------|-----|------|
| Asset volatility (sigma_V) | Computed | sigma_V * 0.75 | sigma_V * 1.25 |
| Debt maturity (T) | 5 years | 3 years | 7 years |
| Risk-free rate (r) | 4.5% | 3.5% | 5.5% |

Present as a 3x3 sensitivity matrix (volatility x maturity or volatility x risk-free rate).

### Interpretation Guidelines

| Metric | Healthy | Moderate Risk | High Risk |
|--------|---------|---------------|-----------|
| Distance to Default (d2) | > 3.0 | 1.5 - 3.0 | < 1.5 |
| Implied Default Prob | < 1% | 1% - 10% | > 10% |
| Merton Value / Market Price | 0.8x - 1.2x | 0.5x - 0.8x or 1.2x - 1.5x | < 0.5x or > 1.5x |

### When Merton Model Is Most Useful

- **High leverage companies**: Debt-to-equity > 1.0 — leverage materially affects equity value
- **Distressed situations**: Companies where default risk is a real concern
- **Financial sector**: Banks, insurance companies where leverage is core business
- **Cross-methodology validation**: Compare Merton value to DCF and Comps values

### When Merton Model Has Limitations

- **Low-debt companies**: If debt is minimal, Merton value converges to market cap (uninformative)
- **Complex capital structures**: Convertible debt, preferred equity, warrants not captured
- **Non-normal distributions**: Assumes log-normal asset returns; tail risk understated

## Methodology 3: Asset-Based Valuation (Net Asset Value)

### Purpose
Value a company by computing the net worth of its tangible and intangible assets minus liabilities. This approach establishes a floor value based on what the company owns, and is particularly useful for asset-heavy firms, holding companies, financial institutions, and liquidation or distressed scenarios.

### When Asset-Based Valuation Is Most Useful

- **Asset-heavy companies**: Real estate, utilities, mining, manufacturing — where tangible assets drive value
- **Financial institutions**: Banks, insurance companies — where book value and tangible book are key metrics
- **Holding companies / conglomerates**: Sum-of-parts NAV is a primary valuation tool
- **Distressed / liquidation analysis**: Tangible book and net-net working capital define downside protection
- **M&A floor pricing**: Acquirers often use asset-based methods to set minimum bid prices

### When Asset-Based Valuation Has Limitations

- **Asset-light companies**: Tech, SaaS, services — value is in earnings power and IP, not balance sheet assets
- **High-growth companies**: Future growth is the primary value driver; NAV is far below market price by design
- **Companies with heavy goodwill**: Acquired goodwill may not reflect realizable value

### Valuation Layers

The asset-based approach produces multiple valuation levels, from most conservative to least:

| Layer | Formula | Use Case |
|-------|---------|----------|
| Net-Net Working Capital (NNWC) | Current Assets - Total Liabilities | Graham deep value floor; ultra-conservative |
| Tangible Book Value (TBV) | Total Equity - Goodwill - Intangible Assets | Liquidation proxy; strips unrealizable intangibles |
| Book Value (BV) | Total Assets - Total Liabilities | GAAP/IFRS equity; standard balance sheet measure |
| Adjusted NAV | Sum of Fair-Value-Adjusted Assets - Total Liabilities | Best estimate of true net asset worth |

### Fair Value Adjustment Factors

When computing Adjusted NAV, apply these adjustment factors to convert book values to estimated fair/realizable values:

| Asset Category | Adjustment Range | Default Factor | Notes |
|----------------|-----------------|----------------|-------|
| Cash & equivalents | 1.00x | 1.00x | Always face value |
| Short-term investments | 0.95-1.00x | 0.98x | Near face value, minor liquidity discount |
| Net receivables | 0.85-0.95x | 0.90x | Discount for bad debts and collection delays |
| Inventory | 0.50-0.80x | 0.65x | Raw materials higher (0.80x), finished goods lower (0.50x); industry-dependent |
| PP&E (net) | 0.60-1.20x | 0.80x | Real estate may appreciate (>1.0x); specialized equipment depreciates faster |
| Goodwill | 0.00-0.50x | 0.00x | Zero in liquidation; partial credit if brand/customer relationships have standalone value |
| Other intangibles | 0.00-0.30x | 0.10x | Patents/IP may retain value (0.20-0.30x); customer lists/non-competes typically zero |
| Long-term investments | 0.80-1.00x | 0.90x | Depends on liquidity; publicly traded at ~1.0x, private holdings discounted |

**Industry-Specific Adjustments:**
- **Real estate**: PP&E may be 1.0x-1.5x book if properties appreciated; use appraised values when available
- **Banks**: Loan portfolio quality is key; adjust receivables based on non-performing loan ratios
- **Retailers**: Inventory often at 0.50-0.60x (seasonal, perishable); real estate leases are off-balance-sheet
- **Manufacturing**: PP&E highly dependent on age, maintenance, and specialization
- **Tech**: Minimal tangible assets; patent portfolio may carry residual value

### Key Ratio Interpretation

| Ratio | Formula | Interpretation |
|-------|---------|---------------|
| Price-to-Book (P/B) | Price / Book Value per Share | < 1.0 = trading below book value (potential value or distress signal) |
| Price-to-Tangible-Book (P/TBV) | Price / Tangible BV per Share | Conservative floor ratio; < 1.0 is noteworthy |
| Price / NNWC | Price / Net-Net Working Capital per Share | < 1.0 = Graham deep value (extremely rare) |
| Price / Adjusted NAV | Price / Adjusted NAV per Share | Best single asset-based metric |
| Tangible Asset Ratio | (Total Assets - Goodwill - Intangibles) / Total Assets | > 70% = asset-heavy (NAV highly informative) |

### Asset Profile Classification

| Tangible Asset Ratio | Classification | NAV Relevance |
|---------------------|----------------|---------------|
| > 70% | Asset-Heavy | NAV is a primary valuation anchor |
| 40% - 70% | Balanced | NAV is moderately informative |
| < 40% | Asset-Light | NAV is a floor value only; earnings-based methods are primary |

## Combining Methodologies

### Four-Pillar Valuation Framework

When all four methodologies are available (DCF, Comps, Merton, Asset-Based):

| Methodology | Default Weight | Best Captures |
|-------------|---------------|---------------|
| DCF (Damodaran) | 35% | Intrinsic value from future cash flows |
| Comparable Comps | 35% | Market-relative value from peers |
| Merton Model | 15% | Leverage-adjusted structural value |
| Asset-Based (NAV) | 15% | Floor value from balance sheet assets |

Adjust weights based on company characteristics:

| Company Type | DCF | Comps | Merton | Asset-Based |
|-------------|-----|-------|--------|-------------|
| Low leverage, profitable | 45% | 35% | 5% | 15% |
| High leverage | 25% | 25% | 35% | 15% |
| Pre-profit / high-growth | 30% | 50% | 10% | 10% |
| Asset-heavy (utilities, REIT, mining) | 25% | 25% | 10% | 40% |
| Financial institutions (banks, insurance) | 20% | 25% | 20% | 35% |
| Distressed / liquidation risk | 15% | 15% | 30% | 40% |
| Asset-light (tech, SaaS, services) | 40% | 40% | 15% | 5% |

### Three-Pillar Valuation Framework (without Asset-Based)

When only DCF, Comps, and Merton are available:

| Methodology | Weight | Best Captures |
|-------------|--------|---------------|
| DCF (Damodaran) | 40% | Intrinsic value from fundamentals |
| Comparable Comps | 40% | Market-relative value from peers |
| Merton Model | 20% | Leverage-adjusted structural value |

Adjust weights based on company characteristics:
- **Low leverage, profitable**: DCF 50%, Comps 40%, Merton 10%
- **High leverage**: DCF 30%, Comps 30%, Merton 40%
- **Pre-profit/high-growth**: DCF 30%, Comps 50%, Merton 20%

### Investor Profile Applications

| Profile | Comps Focus | Merton Focus | Asset-Based Focus |
|---------|-------------|--------------|-------------------|
| **Conservative** | Prefer stocks trading below peer median multiples (margin of safety). Flag any stock where comps-implied value < current price. | Distance to Default must be > 3.0. Reject stocks with implied default prob > 2%. | Require P/TBV < 1.5x. Stocks trading below tangible book are highly attractive. NNWC > 0 is a strong positive. |
| **Moderate** | Accept stocks within +/- 10% of comps-implied fair value. Peer premium justified by superior growth/margins. | Distance to Default > 2.0 acceptable. Default prob < 5% threshold. | P/B < 3.0x acceptable. Tangible asset base provides downside protection. Growing book value is a positive signal. |
| **Aggressive** | Willing to pay premium to peer multiples for growth leaders. Focus on P/S and EV/EBITDA for high-growth names. | Default risk acceptable if equity upside compensates. Focus on Merton-to-market ratio for upside signal. | NAV is less relevant; focus on earnings and growth. P/B > 5x acceptable for companies with strong intangible moats. |

## Brand Color & Styling

All valuation reports MUST use the Agentman brand palette from `references/brand-colors.md`, following the **agentman-pptx-style** design system. Quiet confidence — charcoal suits, not fire trucks.

- **Visual weight**: 70% Carbon/Charcoal, 20% Warm Neutrals, 10% Terracotta accent. Max 3 `AGENTMAN_500` elements per section.
- **Table headers**: `AGENTMAN_100` (#F6EAE6) light fill + `AGENTMAN_500` (#CC785C) terracotta text
- **Table borders**: `AGENTMAN_150` (#E3DACC) warm borders
- **Body text**: `CHARCOAL_950` (#141413); section titles in `CHARCOAL_900` (#292322) with `AGENTMAN_500` (#CC785C) underline
- **Alternating table rows**: `AGENTMAN_50` (#FAF9F5) cream / white; highlight rows in `AGENTMAN_75` (#F0EEE6)
- **Undervalued / discount to peers**: `AGENTMAN_500` (#CC785C) terracotta bold
- **Overvalued / premium to peers**: `AGENTMAN_600` (#A65945) deep terracotta bold
- **Fairly valued / near consensus**: `CHARCOAL_950` (#141413) bold
- **Distance to Default "Healthy"**: `AGENTMAN_500` terracotta; **"High Risk"**: `AGENTMAN_600` deep terracotta; **"Moderate Risk"**: `CHARCOAL_950` bold
- **Verdict boxes**: `AGENTMAN_500` (#CC785C) border + `AGENTMAN_50` (#FAF9F5) cream bg — same style for all verdicts
- **Key valuation metrics** (fair value, intrinsic value): `AGENTMAN_700` (#8B4A38) accent
- **BANNED**: Green, red, amber, blue (except ✓/✗ symbols). No gradients. No invented colors.
