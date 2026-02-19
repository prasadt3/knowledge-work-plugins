---
name: investor-profile-methodology
description: |
  Use when scoring a stock's suitability for different investor types. Provides the complete 50-point scoring
  rubric for Conservative, Moderate, and Aggressive profiles, including thresholds, interpretation guidelines,
  and profile-specific recommendation templates.
---

This skill provides the complete scoring system, thresholds, and interpretation framework for evaluating stocks across three investor risk profiles.

## Investor Profile Definitions

| Attribute | Conservative | Moderate | Aggressive |
|-----------|-------------|----------|------------|
| **Priority** | Capital preservation, income | Balanced growth + income | Capital appreciation, growth |
| **Beta Range** | < 1.0 preferred | 0.8 - 1.3 acceptable | > 1.2 acceptable |
| **DCF Premium Tolerance** | <= 1.1x (margin of safety) | Up to ~1.5x fair value | 2-3x+ for high growth |
| **Drawdown Tolerance** | < 15% | 15-25% | 30%+ |
| **Position Sizing** | 2-5% of portfolio | 3-8% of portfolio | 5-15% of portfolio |
| **Time Horizon** | 5+ years | 2-5 years | Catalyst-driven |
| **Dividend Preference** | High yield, consistent | Some acceptable | Not required |
| **Favored Sectors** | Utilities, staples, healthcare | Sector-agnostic, established growth | Tech, biotech, disruptive |

## Scoring System

Each profile has 5 criteria scored 1-5 (max 10 points per criterion, total 50 points). Each criterion has two sub-components worth up to 5 points each.

### Conservative Profile Scoring (50 pts)

#### 1. Dividend Yield & Consistency (10 pts)
| Sub-Component | 5 pts | 4 pts | 3 pts | 2 pts | 1 pt |
|---------------|-------|-------|-------|-------|------|
| **Current Yield** | >= 3.5% | 2.5-3.4% | 1.5-2.4% | 0.5-1.4% | < 0.5% or none |
| **Dividend Track Record** | 10+ yr growth streak | 5-9 yr growth | Stable payer | Recently started | No dividend / cut |

#### 2. Balance Sheet Strength (10 pts)
| Sub-Component | 5 pts | 4 pts | 3 pts | 2 pts | 1 pt |
|---------------|-------|-------|-------|-------|------|
| **Debt-to-Equity** | < 0.3 | 0.3-0.6 | 0.6-1.0 | 1.0-1.5 | > 1.5 |
| **Current Ratio** | > 2.0 | 1.5-2.0 | 1.2-1.5 | 1.0-1.2 | < 1.0 |

#### 3. Earnings Stability (10 pts)
| Sub-Component | 5 pts | 4 pts | 3 pts | 2 pts | 1 pt |
|---------------|-------|-------|-------|-------|------|
| **EPS Consistency** | 5+ yr consecutive growth | 4 yr growth | Mixed but positive trend | Volatile | Declining |
| **Net Margin** | > 20% | 15-20% | 10-15% | 5-10% | < 5% |

#### 4. Valuation Margin of Safety (10 pts)
| Sub-Component | 5 pts | 4 pts | 3 pts | 2 pts | 1 pt |
|---------------|-------|-------|-------|-------|------|
| **Price vs DCF** | < 0.9x intrinsic | 0.9-1.0x | 1.0-1.1x | 1.1-1.3x | > 1.3x |
| **P/E vs Sector** | > 30% below sector | 15-30% below | Within 15% | 15-30% above | > 30% above |

#### 5. Low Volatility / Beta (10 pts)
| Sub-Component | 5 pts | 4 pts | 3 pts | 2 pts | 1 pt |
|---------------|-------|-------|-------|-------|------|
| **Beta** | < 0.6 | 0.6-0.8 | 0.8-1.0 | 1.0-1.3 | > 1.3 |
| **Max Drawdown (1Y)** | < 10% | 10-15% | 15-20% | 20-30% | > 30% |

### Moderate Profile Scoring (50 pts)

#### 1. Growth-Value Balance / PEG (10 pts)
| Sub-Component | 5 pts | 4 pts | 3 pts | 2 pts | 1 pt |
|---------------|-------|-------|-------|-------|------|
| **PEG Ratio** | < 1.0 | 1.0-1.5 | 1.5-2.0 | 2.0-3.0 | > 3.0 or N/A |
| **Revenue Growth** | 15-25% | 10-15% or 25-35% | 5-10% | 0-5% | Negative |

#### 2. Profitability Quality (10 pts)
| Sub-Component | 5 pts | 4 pts | 3 pts | 2 pts | 1 pt |
|---------------|-------|-------|-------|-------|------|
| **ROE** | > 25% | 18-25% | 12-18% | 8-12% | < 8% |
| **Operating Margin** | > 25% | 18-25% | 12-18% | 5-12% | < 5% |

#### 3. Analyst Consensus Strength (10 pts)
| Sub-Component | 5 pts | 4 pts | 3 pts | 2 pts | 1 pt |
|---------------|-------|-------|-------|-------|------|
| **Consensus Rating** | Strong Buy | Buy | Outperform | Hold | Sell/Underperform |
| **Analyst Upside** | > 25% | 15-25% | 10-15% | 0-10% | Negative |

#### 4. Reasonable Valuation (10 pts)
| Sub-Component | 5 pts | 4 pts | 3 pts | 2 pts | 1 pt |
|---------------|-------|-------|-------|-------|------|
| **P/E (TTM)** | < 15 | 15-20 | 20-30 | 30-40 | > 40 |
| **Price vs DCF** | < 1.0x intrinsic | 1.0-1.2x | 1.2-1.5x | 1.5-2.0x | > 2.0x |

#### 5. Risk-Adjusted Return Potential (10 pts)
| Sub-Component | 5 pts | 4 pts | 3 pts | 2 pts | 1 pt |
|---------------|-------|-------|-------|-------|------|
| **Beta** | 0.8-1.0 | 1.0-1.2 or 0.6-0.8 | 1.2-1.4 or 0.4-0.6 | 1.4-1.6 | > 1.6 or < 0.4 |
| **1Y Return** | > 20% | 10-20% | 0-10% | -10-0% | < -10% |

### Aggressive Profile Scoring (50 pts)

#### 1. Revenue Growth Rate (10 pts)
| Sub-Component | 5 pts | 4 pts | 3 pts | 2 pts | 1 pt |
|---------------|-------|-------|-------|-------|------|
| **YoY Revenue Growth** | > 40% | 25-40% | 15-25% | 5-15% | < 5% |
| **Revenue Acceleration** | Accelerating QoQ | Stable high growth | Stable moderate | Decelerating | Stagnant/declining |

#### 2. Market Position & TAM (10 pts)
| Sub-Component | 5 pts | 4 pts | 3 pts | 2 pts | 1 pt |
|---------------|-------|-------|-------|-------|------|
| **Market Share Trajectory** | Gaining rapidly | Gaining steadily | Maintaining | Losing slowly | Losing rapidly |
| **TAM Expansion** | Large & expanding | Large & stable | Moderate & growing | Niche | Shrinking |

#### 3. Momentum & Technical Strength (10 pts)
| Sub-Component | 5 pts | 4 pts | 3 pts | 2 pts | 1 pt |
|---------------|-------|-------|-------|-------|------|
| **3M Price Return** | > 25% | 15-25% | 5-15% | -5-5% | < -5% |
| **Price vs 50-Day MA** | > 10% above | 5-10% above | Near MA (+/-5%) | 5-10% below | > 10% below |

#### 4. Innovation / Disruption Potential (10 pts)
| Sub-Component | 5 pts | 4 pts | 3 pts | 2 pts | 1 pt |
|---------------|-------|-------|-------|-------|------|
| **Product Pipeline** | Multiple catalysts | Strong pipeline | Moderate pipeline | Incremental only | No visible pipeline |
| **Competitive Disruption** | Category creator | Disruptor gaining share | Fast follower | Established player | Legacy incumbent |

#### 5. Upside to Price Targets (10 pts)
| Sub-Component | 5 pts | 4 pts | 3 pts | 2 pts | 1 pt |
|---------------|-------|-------|-------|-------|------|
| **Analyst High Target Upside** | > 50% | 30-50% | 15-30% | 5-15% | < 5% |
| **Buy Rating %** | > 80% | 65-80% | 50-65% | 35-50% | < 35% |

## Score Interpretation

| Score Range | Rating | Interpretation |
|-------------|--------|----------------|
| **40-50** | Excellent Fit | Strongly suited for this investor profile |
| **30-39** | Good Fit | Well-suited with minor trade-offs |
| **20-29** | Moderate Fit | Some alignment but notable gaps |
| **10-19** | Poor Fit | Significant misalignment with profile goals |
| **0-9** | Not Suitable | Fundamentally incompatible with profile |

## Valuation Approach by Profile

### Conservative: Margin of Safety
- Require stock to trade at or below intrinsic value (DCF <= 1.1x)
- Weight dividend yield and balance sheet heavily
- Use analyst low/median price target as reference
- Prefer stocks with narrow analyst target spread (high certainty)

### Moderate: Fair Value with Growth
- Accept modest premium for quality growth (DCF up to ~1.5x)
- Balance P/E and growth rate via PEG ratio
- Use analyst median price target as primary reference
- Look for profitability inflection points

### Aggressive: Growth Premium Acceptable
- Accept significant premium for high-growth names (DCF 2-3x+)
- Focus on revenue acceleration and TAM expansion
- Use analyst high price target and momentum signals
- Tolerate current unprofitability if path to margins is clear

## Recommendation Templates

### Conservative Fit
- **Excellent/Good Fit**: "Suitable for conservative portfolios seeking [income/stability]. Position sizing: 3-5% with [stop-loss consideration]."
- **Moderate Fit**: "Partial allocation possible with awareness of [specific gap]. Consider pairing with [hedge]."
- **Poor Fit / Not Suitable**: "Does not meet conservative criteria due to [specific reasons]. Consider [alternative sector/type] instead."

### Moderate Fit
- **Excellent/Good Fit**: "Well-suited for balanced portfolios. Offers [growth + value characteristic]. Position sizing: 4-7%."
- **Moderate Fit**: "Acceptable with portfolio context. Monitor [metric] for improvement."
- **Poor Fit / Not Suitable**: "Risk/reward doesn't align with moderate profile. [Too aggressive because X] or [too conservative, missing Y]."

### Aggressive Fit
- **Excellent/Good Fit**: "Strong growth candidate for aggressive portfolios. High-conviction position sizing: 5-12%. Key catalyst: [event]."
- **Moderate Fit**: "Growth potential present but [momentum/disruption] signals are mixed. Smaller position: 3-5%."
- **Poor Fit / Not Suitable**: "Insufficient growth or momentum for aggressive allocation. [Revenue growth too slow] or [limited upside catalyst]."

## Brand Color & Styling

All profile scoring output MUST use the Agentman brand palette from `references/brand-colors.md`, following the **agentman-pptx-style** design system. Quiet confidence — charcoal suits, not fire trucks. See `references/color-antipatterns.md` for forbidden patterns.

### Visual Weight
70% Carbon/Charcoal, 20% Warm Neutrals, 10% Terracotta accent. Max 3 `AGENTMAN_500` elements per section.

### Table Structure
- **Table headers**: `AGENTMAN_100` (#F6EAE6) light fill, `AGENTMAN_500` (#CC785C) terracotta text
- **Body text**: `CHARCOAL_950` (#141413); section titles in `CHARCOAL_900` (#292322) with `AGENTMAN_500` (#CC785C) underline
- **Alternating table rows**: `AGENTMAN_50` (#FAF9F5) cream / white; best-fit row in `AGENTMAN_75` (#F0EEE6)
- **Table borders**: `AGENTMAN_150` (#E3DACC) warm

### Score Tier Badges
All badges use the same warm base — **no color-coded tiers**:
- `AGENTMAN_100` (#F6EAE6) background, `AGENTMAN_800` (#703B2D) text, `AGENTMAN_200` (#E6A890) border, `border-radius: 4px`
- Tier differentiation via text wording only ("Excellent Fit", "Good Fit", "Moderate Fit", etc.)

### Score Bars
- **Track**: `AGENTMAN_150` (#E3DACC), 6px height
- **Fill**: `AGENTMAN_500` (#CC785C) terracotta — same for ALL tiers

### Emphasis Text (replaces semantic colors)
- Positive/Buy: `AGENTMAN_500` (#CC785C) terracotta bold
- Negative/Avoid: `AGENTMAN_600` (#A65945) deep terracotta bold
- Caution/Mixed: `AGENTMAN_400` (#D97757) warm highlight
- Neutral/Hold: `CHARCOAL_950` (#141413) bold

### Banned Colors
Green (#10B981), red (#EF4444), amber (#F59E0B), and blue (#3B82F6) are **BANNED** from reports. The ONE exception: ✓/✗ comparison symbols (green ✓, red ✗ — symbols only, not text).

### Critical Rules
- **No semantic colors** — use terracotta-family emphasis instead
- **No gradients** — solid fills only
- **No invented colors** — every hex must trace to `brand-colors.md`
- **No colored headings** — headings are always charcoal
- **Terracotta budget** — max 3 `AGENTMAN_500` elements per section
