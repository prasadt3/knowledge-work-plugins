# Color Antipatterns — What NOT to Do

This document lists **forbidden color usage patterns** for Agentman equity research reports. All generated PDF and DOCX output MUST avoid these antipatterns.

These rules derive from the Agentman brand system:
- **agentman-pptx-style**: "Quiet confidence — charcoal suits, not fire trucks." 70/20/10 visual weight. Semantic colors banned. Terracotta budget of 3 elements per section.
- **agentman-brand-voice**: "Calm, earned confidence — we've done the work, we don't need to shout." "Reassuring before impressive — trust first, admiration second."
- **brand-colors.md**: Warm terracotta/cream palette. Green/red/amber/blue banned except comparison ✓/✗ symbols.

**Rule**: If a color is not defined in `brand-colors.md`, it MUST NOT appear in any report. When in doubt, use charcoal for text and cream for backgrounds — never reach for semantic colors.

---

## Antipattern 1: Using Semantic Colors (Green/Red/Amber/Blue)

**NEVER** use green (#10B981), red (#EF4444), amber (#F59E0B), or blue (#3B82F6) in reports. These colors break the quiet confidence aesthetic and create a dashboard/alert feel that is inappropriate for boardroom-ready research.

### Bad Example
```css
/* WRONG — semantic colors create traffic-light / dashboard aesthetic */
.positive-value { color: #10B981; }      /* green for gains */
.negative-value { color: #EF4444; }      /* red for losses */
.caution-value { color: #F59E0B; }       /* amber for mixed */
.info-highlight { color: #3B82F6; }      /* blue for informational */
```

### Correct Example
```css
/* RIGHT — terracotta family for ALL emphasis */
.positive-value { color: #CC785C; font-weight: 700; }   /* AGENTMAN_500 — emphasis */
.negative-value { color: #A65945; font-weight: 700; }   /* AGENTMAN_600 — concern/negative */
.caution-value { color: #D97757; }                       /* AGENTMAN_400 — highlight */
.neutral-value { color: #141413; }                       /* CHARCOAL_950 — default */
```

### The ONE Exception: Comparison ✓/✗ Symbols
```css
/* ONLY permitted use of green/red — comparison table symbols ONLY */
.checkmark { color: #10B981; font-weight: bold; }  /* ✓ symbol only */
.crossmark { color: #EF4444; font-weight: bold; }  /* ✗ symbol only */
.checkmark-text { color: #CC785C; }                 /* AGENTMAN_500 — text after ✓ */
.crossmark-text { color: #A65945; }                 /* AGENTMAN_600 — text after ✗ */
```

**Why**: Per `agentman-pptx-style`, green/red/amber/blue "break the quiet confidence aesthetic" and are "banned in presentations." The terracotta family provides sufficient emphasis range without creating visual noise.

---

## Antipattern 2: Dark Table Headers

**NEVER** use dark-filled table headers with white text. The PPTX-style uses light, warm table headers.

### Bad Example
```css
/* WRONG — dark table headers feel heavy and generic */
th { background: #703B2D; color: white; }     /* AGENTMAN_800 dark fill */
th { background: #292322; color: white; }     /* charcoal dark fill */
th { background: #1B3A5C; color: white; }     /* navy fill */
```

### Correct Example
```css
/* RIGHT — light warm fill with terracotta text (agentman-pptx-style) */
th {
  background: #F6EAE6;   /* AGENTMAN_100 — light brand fill */
  color: #CC785C;         /* AGENTMAN_500 — terracotta text */
  font-weight: 600;
  border-bottom: 1px solid #E3DACC;  /* AGENTMAN_150 border */
}
```

**Why**: Light table headers feel refined and editorial. Dark headers feel like dashboards. The `agentman-pptx-style` specifies `brand-100` fill with `brand-500` text for all branded tables.

---

## Antipattern 3: Saturated Color-Fill Badges

**NEVER** use bright, fully-saturated background colors for badges, pills, or tier indicators.

### Bad Example
```css
/* WRONG — saturated fills create garish "rainbow" effect */
.badge-excellent { background: #10B981; color: white; }
.badge-good { background: #CC785C; color: white; }
.badge-moderate { background: #F59E0B; color: white; }
.badge-poor { background: #EF4444; color: white; }
```

### Correct Example
```css
/* RIGHT — muted brand badges, same base for all tiers */
.badge {
  background: #F6EAE6;           /* AGENTMAN_100 */
  color: #703B2D;                /* AGENTMAN_800 */
  border: 1px solid #E6A890;    /* AGENTMAN_200 */
  padding: 3px 10px;
  border-radius: 4px;
  font-size: 12px;
  font-weight: 600;
}
/* Tier differentiation via TEXT WORDING, not color. All badges look identical. */
```

**Why**: The `agentman-pptx-style` bans semantic colors entirely. All badges share the same warm brand base. The tier signal comes from the badge text ("Excellent Fit", "Moderate Fit"), not from color coding.

---

## Antipattern 4: Exceeding the Terracotta Budget

**NEVER** use more than 3 `AGENTMAN_500` (#CC785C) elements per section or table. Terracotta loses impact when overused.

### What Counts as a Brand-500 Element
- Each stat number in terracotta
- Each standalone accent line or section divider
- Each table header row (counts as 1)
- Each badge cluster (counts as 1)
- Emphasis text when using brand-500

### What Does NOT Count
- Structural elements (alternating row fills, borders)
- Footer text (uses slate-500)
- Body text in charcoal

### Bad Example
```html
<!-- WRONG — 5 terracotta elements in one section -->
<h3 style="border-bottom: 3px solid #CC785C">Title</h3>        <!-- 1 -->
<div style="color:#CC785C;font-size:34px">94%</div>             <!-- 2 -->
<div style="color:#CC785C;font-size:34px">$2.5B</div>           <!-- 3 -->
<div style="color:#CC785C;font-size:34px">12.5x</div>           <!-- 4 -->
<span style="color:#CC785C">Compelling Long</span>               <!-- 5 -->
```

### Correct Example
```html
<!-- RIGHT — 3 terracotta elements, charcoal for the rest -->
<h3 style="color:#292322;border-bottom:3px solid #CC785C">Title</h3>  <!-- 1 -->
<div style="color:#CC785C;font-size:34px">94%</div>                    <!-- 2 -->
<div style="color:#141413;font-size:28px">$2.5B</div>                  <!-- charcoal, not counted -->
<div style="color:#141413;font-size:28px">12.5x</div>                  <!-- charcoal, not counted -->
<span style="color:#CC785C">Compelling Long</span>                      <!-- 3 — max reached -->
```

**Why**: Per `agentman-pptx-style`, "Terracotta loses impact when overused. It must feel rare."

---

## Antipattern 5: Gradients Anywhere

**NEVER** use gradients on any element — backgrounds, cards, text, accent bars, or graphics.

### Bad Example
```css
/* WRONG */
.header { background: linear-gradient(135deg, #703B2D, #CC785C); }
.text { background: linear-gradient(to right, #CC785C, #D97757); -webkit-background-clip: text; }
```

### Correct Example
```css
/* RIGHT — solid fills only */
.header { background: #F6EAE6; }
.accent { background: #CC785C; }
```

**Why**: Per `agentman-pptx-style`, "Gradients are AI-generated hallmarks. Solid fills feel editorial and confident."

---

## Antipattern 6: Inventing Colors Not in the Palette

**NEVER** introduce hex values that are not defined in `brand-colors.md`.

| Forbidden Color | Why It Appears | Correct Replacement |
|---|---|---|
| `#f0f7ff` | Light blue tint for highlight boxes | `#FAF9F5` (AGENTMAN_50 cream) |
| `#E8F0FE` | Light blue row background | `#F0EEE6` (AGENTMAN_75 warm cream) |
| `#EFF6FF` | Info box background | `#FAF9F5` (AGENTMAN_50 cream) |
| `#DBEAFE` | Blue badge background | `#F6EAE6` (AGENTMAN_100 light brand) |
| `#ECFDF5` | Light green badge fill | `#F6EAE6` (AGENTMAN_100) |
| `#FEF3C7` | Light amber badge fill | `#FAF9F5` (AGENTMAN_50) |
| `#FEF2F2` | Light red badge fill | `#FAF9F5` (AGENTMAN_50) |
| `#1D4ED8` | Dark blue accent | `#703B2D` (AGENTMAN_800) |
| `#2563EB` | Medium blue link | `#CC785C` (AGENTMAN_500) |
| `#333333` | Generic dark gray | `#141413` (CHARCOAL_950) |
| `#666666` | Generic medium gray | `#475569` (SLATE_600) |
| `#F5F5F5` | Generic light gray | `#FAF9F5` (AGENTMAN_50 cream) |

**Rule**: Every hex value in a report must trace back to a named constant in `brand-colors.md`.

---

## Antipattern 7: Colored Section Headings

**NEVER** color section headings with any color other than charcoal. Headings are structural, not decorative.

### Bad Example
```css
/* WRONG */
h3.conservative { color: #3B82F6; }    /* blue heading */
h3.bullish { color: #10B981; }         /* green heading */
h2.bearish { color: #EF4444; }         /* red heading */
h2.section { color: #CC785C; }         /* terracotta heading */
```

### Correct Example
```css
/* RIGHT — headings are always charcoal */
h2 { color: #292322; border-bottom: 3px solid #CC785C; }  /* CHARCOAL_900 + terracotta underline */
h3 { color: #292322; }                                     /* CHARCOAL_900 */
```

**Why**: Section headings use charcoal text hierarchy. The terracotta underline provides brand accent without coloring the heading text itself.

---

## Antipattern 8: Highlight Boxes with Non-Brand Colors

**NEVER** use blue, green, red, or any non-brand color for highlight box borders or backgrounds.

### Bad Example
```css
/* WRONG */
.highlight { border: 2px solid #3B82F6; background: #f0f7ff; }
.callout { border: 2px solid #10B981; background: #ECFDF5; }
```

### Correct Example
```css
/* RIGHT — cream fill with terracotta border (agentman-pptx-style callout block) */
.highlight { border: 2px solid #CC785C; background: #F0EEE6; }  /* brand-500 border + brand-75 fill */
.highlight h3 { color: #292322; font-weight: bold; }            /* charcoal heading */
.highlight p { color: #475569; }                                 /* slate-600 body */
```

**Why**: Callout/highlight boxes follow the PPTX-style callout block pattern: warm cream fill with charcoal text. The box itself provides emphasis; internal content stays neutral.

---

## Correct Table Styling Reference

### Table Structure (agentman-pptx-style)
```css
/* Table headers — light warm fill with terracotta text */
th {
  background: #F6EAE6;           /* AGENTMAN_100 */
  color: #CC785C;                 /* AGENTMAN_500 */
  font-weight: 600;
  font-size: 13px;
  padding: 10px 14px;
  border-bottom: 1px solid #E3DACC;  /* AGENTMAN_150 */
}

/* Rows — warm alternating, never gray or blue */
tr:nth-child(even) td { background: #FAF9F5; }  /* AGENTMAN_50 cream */
tr:nth-child(odd) td { background: white; }
tr.highlight td { background: #F0EEE6; }         /* AGENTMAN_75 warm cream */

/* Borders — warm, not cold */
td { border-bottom: 1px solid #E3DACC; padding: 9px 14px; }  /* AGENTMAN_150 */
```

### Badge Pattern
```css
/* ALL badges use the same warm base — no color-coded tiers */
.badge {
  background: #F6EAE6;           /* AGENTMAN_100 */
  color: #703B2D;                /* AGENTMAN_800 */
  border: 1px solid #E6A890;    /* AGENTMAN_200 */
  padding: 3px 10px;
  border-radius: 4px;
  font-size: 12px;
  font-weight: 600;
}
/* Tier differentiation via text label only, not via color */
```

### Score Bars
```css
.score-bar { background: #E3DACC; height: 6px; border-radius: 3px; }    /* AGENTMAN_150 track */
.score-fill { background: #CC785C; height: 6px; border-radius: 3px; }   /* AGENTMAN_500 fill — ALL tiers */
```

### Emphasis Text (replaces semantic color text)
```css
.emphasis-positive { color: #CC785C; font-weight: 700; }   /* AGENTMAN_500 — positive/buy/upside */
.emphasis-negative { color: #A65945; font-weight: 700; }   /* AGENTMAN_600 — negative/avoid/downside */
.emphasis-highlight { color: #D97757; font-weight: 600; }  /* AGENTMAN_400 — caution/highlight */
.emphasis-neutral { color: #141413; font-weight: 600; }    /* CHARCOAL_950 — hold/neutral */
```

### Comparison Table (✓/✗ — only place green/red is allowed)
```css
/* Positive column */
.check-symbol { color: #10B981; font-weight: bold; }   /* green ✓ only */
.check-text { color: #CC785C; }                         /* AGENTMAN_500 */

/* Negative column */
.cross-symbol { color: #EF4444; font-weight: bold; }   /* red ✗ only */
.cross-text { color: #A65945; }                         /* AGENTMAN_600 */
```

### Callout/Highlight Block (agentman-pptx-style)
```css
.callout-block {
  background: #F0EEE6;     /* AGENTMAN_75 cream */
  border-radius: 4px;
  padding: 16px 20px;
}
.callout-block h3 { color: #141413; font-weight: bold; }  /* CHARCOAL_950 */
.callout-block p { color: #475569; }                        /* SLATE_600 */
```

---

## Allowed Color Usage Summary

| Element Type | Allowed Colors |
|---|---|
| **Table headers** | `AGENTMAN_100` (#F6EAE6) fill + `AGENTMAN_500` (#CC785C) text |
| **Table borders** | `AGENTMAN_150` (#E3DACC) warm separators |
| **Section headings** | `CHARCOAL_900` (#292322) text + `AGENTMAN_500` (#CC785C) underline |
| **Body text** | `CHARCOAL_950` (#141413) or `SLATE_600` (#475569) |
| **Secondary text** | `SLATE_600` (#475569) |
| **Meta/footer** | `SLATE_500` (#64748B) |
| **Alternating rows** | `AGENTMAN_50` (#FAF9F5) cream / white |
| **Highlight rows** | `AGENTMAN_75` (#F0EEE6) warm cream |
| **Badges (all tiers)** | `AGENTMAN_100` bg + `AGENTMAN_800` text + `AGENTMAN_200` border |
| **Score bars** | `AGENTMAN_150` track + `AGENTMAN_500` fill |
| **Stat numbers** | `AGENTMAN_500` (#CC785C) always |
| **Emphasis (positive)** | `AGENTMAN_500` (#CC785C) terracotta |
| **Emphasis (negative)** | `AGENTMAN_600` (#A65945) deep terracotta |
| **Emphasis (highlight)** | `AGENTMAN_400` (#D97757) warm highlight |
| **Verdict text** | Terracotta family only — never green/red |
| **Callout blocks** | `AGENTMAN_75` bg + `CHARCOAL_950` text |
| **Accent lines** | `AGENTMAN_500` (#CC785C) — max 3 per section |
| **Comparison ✓/✗** | Green/red for SYMBOLS ONLY, terracotta for text |

---

## Quick Self-Check for Generated Reports

Before finalizing any report, verify:

1. **No green, red, amber, or blue** anywhere except ✓/✗ comparison symbols
2. **Table headers are light** — `AGENTMAN_100` fill + `AGENTMAN_500` text, NOT dark fill + white text
3. **Table borders are warm** — `AGENTMAN_150` (#E3DACC), not slate
4. **No invented hex values** — every color traces to `brand-colors.md`
5. **Headings are charcoal** (#292322), never colored
6. **Terracotta budget**: ≤3 `AGENTMAN_500` elements per section
7. **No gradients** anywhere — solid fills only
8. **All backgrounds are white or cream** (#FFFFFF, #FAF9F5, #F0EEE6, #F6EAE6)
9. **Visual weight feels 70/20/10** — mostly charcoal, some cream, rare terracotta
10. **Overall feel is quiet confidence** — boardroom-ready, not dashboard-busy
