# Agentman Brand Color System for Equity Research Reports

This file defines the official Agentman brand color palette for use in all generated **PDF and DOCX** reports. These colors are sourced from the `agentman-pptx-style` and `agentman-brand-voice` skills.

**MANDATORY**: All report generation scripts MUST use these brand colors instead of generic blue/gray palettes — whether generating PDF (via `reportlab`, `fpdf2`, `weasyprint`) or DOCX (via `python-docx`). The brand identity is **quiet confidence** — charcoal suits, not fire trucks. Carbon and warm neutrals do the heavy lifting. Terracotta appears as a rare, deliberate accent.

## Visual Weight Distribution

Every report must maintain this ratio:

- **70% Carbon/Charcoal** (`141413`, `292322`, `3D3735`) — the backbone
- **20% Warm Neutrals** (`F0EEE6`, `F6EAE6`, `E3DACC`, `FAF9F5`, `FFFFFF`) — warmth without color
- **10% Terracotta Accent** (`CC785C`, `D97757`, `A65945`) — sparingly

## Report Color Constants (PDF and DOCX)

Copy-paste these constants into any report generation script (PDF via reportlab/fpdf2/weasyprint, or DOCX via python-docx/docx-js):

```javascript
// ============================================================
// AGENTMAN BRAND COLORS — Official Palette
// Source: agentman-pptx-style (colors.md)
// ============================================================

// Primary Brand (Terracotta Orange) — USE SPARINGLY, max 3 elements per section
const AGENTMAN_800 = "703B2D";   // Deep emphasis (rare)
const AGENTMAN_700 = "8B4A38";   // Text on light backgrounds (rare), metric box values
const AGENTMAN_600 = "A65945";   // Accent bars, secondary emphasis
const AGENTMAN_500 = "CC785C";   // PRIMARY ACCENT — stat numbers, table header text, accent lines, CTA. MAX 3 PER SECTION.
const AGENTMAN_400 = "D97757";   // Highlight text, key phrases, callout statements
const AGENTMAN_200 = "E6A890";   // Borders, subtle accents
const AGENTMAN_150 = "E3DACC";   // TABLE BORDERS, separators on light backgrounds
const AGENTMAN_100 = "F6EAE6";   // TABLE HEADER FILL, icon containers, badge backgrounds
const AGENTMAN_75  = "F0EEE6";   // HIGHLIGHT ROW BG — callout blocks, cream backgrounds
const AGENTMAN_50  = "FAF9F5";   // ALTERNATE ROW BG — very light cream

// Text Colors (Charcoal) — 70% of visual weight
const CHARCOAL_950 = "141413";   // PRIMARY TEXT — body copy, headings on light
const CHARCOAL_900 = "292322";   // Section titles, cover title
const CHARCOAL_800 = "3D3735";   // Secondary text, card accent bars

// Neutral (Slate)
const SLATE_700    = "334155";   // Secondary text on very light backgrounds
const SLATE_600    = "475569";   // Body text on white/cream
const SLATE_500    = "64748B";   // Footer text, muted captions
const SLATE_400    = "94A3B8";   // Descriptions, meta text
const SLATE_300    = "CBD5E1";   // Emphasized text on dark backgrounds
const SLATE_200    = "E2E8F0";   // Borders on light (secondary to AGENTMAN_150)
const SLATE_100    = "F1F5F9";   // Light backgrounds
const WHITE        = "FFFFFF";

// BANNED COLORS — Do NOT use in reports
// const SUCCESS   = "10B981";  // BANNED — except ✓ symbols in comparison tables
// const WARNING   = "F59E0B";  // BANNED — breaks quiet confidence aesthetic
// const ERROR     = "EF4444";  // BANNED — except ✗ symbols in comparison tables
// const INFO      = "3B82F6";  // BANNED — generic corporate, dilutes brand
```

## Element-to-Color Mapping

| Report Element | Agentman Color | Hex | Constant |
|---|---|---|---|
| Table header fill | Light brand | #F6EAE6 | `AGENTMAN_100` |
| Table header text | Primary terracotta | #CC785C | `AGENTMAN_500` |
| Table borders | Warm separator | #E3DACC | `AGENTMAN_150` |
| Section title text | Charcoal dark | #292322 | `CHARCOAL_900` |
| Section title underline | Primary terracotta | #CC785C | `AGENTMAN_500` |
| Body text | Charcoal primary | #141413 | `CHARCOAL_950` |
| Body text (secondary) | Slate medium | #475569 | `SLATE_600` |
| Subheading text | Charcoal medium | #3D3735 | `CHARCOAL_800` |
| Meta/footer text | Slate muted | #64748B | `SLATE_500` |
| Header/footer rule | Primary terracotta | #CC785C | `AGENTMAN_500` |
| Key/highlight row bg | Warm cream | #F0EEE6 | `AGENTMAN_75` |
| Alternate row bg | Light cream | #FAF9F5 | `AGENTMAN_50` |
| Cover page title | Charcoal dark | #292322 | `CHARCOAL_900` |
| Cover page accent | Terracotta | #8B4A38 | `AGENTMAN_700` |
| Metric box background | Warm cream | #F0EEE6 | `AGENTMAN_75` |
| Metric box values | Primary terracotta | #CC785C | `AGENTMAN_500` |
| Metric box labels | Slate medium | #475569 | `SLATE_600` |
| Stat numbers | Primary terracotta (always) | #CC785C | `AGENTMAN_500` |
| Stat labels | Charcoal primary | #141413 | `CHARCOAL_950` |
| Accent lines/bars | Primary terracotta | #CC785C | `AGENTMAN_500` |
| Callout block fill | Warm cream | #F0EEE6 | `AGENTMAN_75` |
| Callout block text | Charcoal primary | #141413 | `CHARCOAL_950` |
| Badge background | Light brand | #F6EAE6 | `AGENTMAN_100` |
| Badge text | Deep terracotta | #703B2D | `AGENTMAN_800` |
| Badge border | Subtle accent | #E6A890 | `AGENTMAN_200` |
| Score bars (track) | Warm separator | #E3DACC | `AGENTMAN_150` |
| Score bars (fill) | Primary terracotta | #CC785C | `AGENTMAN_500` |
| Emphasis text (positive) | Primary terracotta | #CC785C | `AGENTMAN_500` |
| Emphasis text (negative) | Deep terracotta | #A65945 | `AGENTMAN_600` |
| Comparison ✓ symbol | Green (ONLY for symbol) | #10B981 | Exception |
| Comparison ✗ symbol | Red (ONLY for symbol) | #EF4444 | Exception |
| Comparison ✓ text | Primary terracotta | #CC785C | `AGENTMAN_500` |
| Comparison ✗ text | Secondary terracotta | #A65945 | `AGENTMAN_600` |

## Banned Colors

Per the `agentman-pptx-style`, the following colors are **banned from reports** — they break the quiet confidence aesthetic:

| Color | Hex | Why Banned |
|---|---|---|
| Green (success) | #10B981 | Traffic-light aesthetic, too bright (except ✓ symbol) |
| Amber (warning) | #F59E0B | Dashboard alert feel, too bright |
| Red (error) | #EF4444 | Alarm aesthetic, breaks boardroom tone (except ✗ symbol) |
| Blue (info) | #3B82F6 | Generic corporate, dilutes brand |
| Cyan | #0891B2 | Too techy |
| Any gradient | N/A | Banned entirely. Solid fills only. |

### The ONE Exception: Comparison Symbols

When showing ✓/✗ patterns in comparison tables (e.g., "Strengths" vs "Risks"), muted green (#10B981) and muted red (#EF4444) are permitted **for the checkmark/cross symbols only** — never for backgrounds, borders, body text, or any other element.

**Rules for the exception:**
- Green/red ONLY for the ✓ and ✗ characters themselves
- The text following the symbol uses terracotta family: `AGENTMAN_500` (positive) and `AGENTMAN_600` (negative)
- Backgrounds remain white/cream alternating rows
- Borders use `AGENTMAN_150` (warm separators)
- This exception does NOT extend to other table types, badges, verdict text, headings, or backgrounds

## Design Principles

These principles derive from the **agentman-pptx-style** ("quiet confidence — charcoal suits, not fire trucks") and **agentman-brand-voice** ("calm, earned confidence," "reassuring before impressive"). See `color-antipatterns.md` for the full list of forbidden patterns.

1. **Quiet confidence**: Carbon and warm neutrals do the heavy lifting. Terracotta appears as a rare, deliberate accent. The brand feels boardroom-ready, not dashboard-busy.
2. **70/20/10 visual weight**: 70% charcoal (text, structure), 20% warm neutrals (cream/tan backgrounds, borders), 10% terracotta accent (stat numbers, header text, accent bars).
3. **Terracotta budget**: Max 3 `AGENTMAN_500` elements per section/table. Count: each stat number, each accent line, each table header row (as one), each badge cluster (as one). Terracotta loses impact when overused.
4. **Warm table headers**: `AGENTMAN_100` (#F6EAE6) light fill with `AGENTMAN_500` (#CC785C) text — not dark headers. This is the PPTX-style table pattern.
5. **Warm borders**: `AGENTMAN_150` (#E3DACC) for table borders and separators. Not cold slate.
6. **No semantic colors**: Green, red, amber, and blue are banned from reports. These break the boardroom tone. Use terracotta-family emphasis (`AGENTMAN_500` for positive, `AGENTMAN_600` for negative) instead.
7. **No gradients**: Solid fills only. Gradients are AI-generated hallmarks.
8. **No invented colors**: Every hex value must trace to a named constant above.
9. **Text hierarchy**: `CHARCOAL_950` body → `CHARCOAL_900` headings → `SLATE_600` secondary → `SLATE_500` meta/footer. Headings are NEVER colored.
10. **Badges use brand palette only**: `AGENTMAN_100` bg + `AGENTMAN_800` text + `AGENTMAN_200` border. Tier signal via text wording, not color coding.

## DOCX Implementation Guide (python-docx)

When generating DOCX reports with `python-docx`, apply the brand colors using these patterns:

```python
from docx import Document
from docx.shared import Pt, Inches, RGBColor
from docx.oxml.ns import qn
from docx.enum.table import WD_TABLE_ALIGNMENT

# ============================================================
# AGENTMAN BRAND COLORS — python-docx RGBColor Constants
# ============================================================
AGENTMAN_800 = RGBColor(0x70, 0x3B, 0x2D)   # Deep emphasis
AGENTMAN_700 = RGBColor(0x8B, 0x4A, 0x38)   # Cover accent
AGENTMAN_600 = RGBColor(0xA6, 0x59, 0x45)   # Negative emphasis
AGENTMAN_500 = RGBColor(0xCC, 0x78, 0x5C)   # PRIMARY ACCENT
AGENTMAN_400 = RGBColor(0xD9, 0x77, 0x57)   # Highlight text
AGENTMAN_200 = RGBColor(0xE6, 0xA8, 0x90)   # Badge border
AGENTMAN_150 = RGBColor(0xE3, 0xDA, 0xCC)   # Table borders
AGENTMAN_100 = RGBColor(0xF6, 0xEA, 0xE6)   # Table header fill
AGENTMAN_75  = RGBColor(0xF0, 0xEE, 0xE6)   # Highlight row bg
AGENTMAN_50  = RGBColor(0xFA, 0xF9, 0xF5)   # Alternate row bg

CHARCOAL_950 = RGBColor(0x14, 0x14, 0x13)   # Primary text
CHARCOAL_900 = RGBColor(0x29, 0x23, 0x22)   # Section titles
CHARCOAL_800 = RGBColor(0x3D, 0x37, 0x35)   # Secondary text

SLATE_600    = RGBColor(0x47, 0x55, 0x69)   # Body text secondary
SLATE_500    = RGBColor(0x64, 0x74, 0x8B)   # Footer/meta text

# Table header cell shading (apply to each header cell):
def set_cell_shading(cell, hex_color):
    """Apply background shading to a DOCX table cell."""
    shading = cell._element.get_or_add_tcPr()
    shading_elm = shading.makeelement(qn('w:shd'), {
        qn('w:fill'): hex_color,
        qn('w:val'): 'clear',
    })
    shading.append(shading_elm)

# Example: Style a table header row
# for cell in table.rows[0].cells:
#     set_cell_shading(cell, 'F6EAE6')  # AGENTMAN_100
#     for paragraph in cell.paragraphs:
#         for run in paragraph.runs:
#             run.font.color.rgb = AGENTMAN_500
#             run.font.bold = True

# Document metadata:
# doc.core_properties.author = "Agentman Equity Research Assistant"
# doc.core_properties.title = "Agentman — {Report Title}"
```

### DOCX Element Mapping

| Report Element | python-docx Implementation |
|---|---|
| Table header fill | `set_cell_shading(cell, 'F6EAE6')` |
| Table header text | `run.font.color.rgb = AGENTMAN_500` |
| Table borders | `set_cell_shading` for borders using `'E3DACC'` |
| Section titles | `run.font.color.rgb = CHARCOAL_900` + add bottom border paragraph |
| Body text | `run.font.color.rgb = CHARCOAL_950` |
| Alternate row bg | `set_cell_shading(cell, 'FAF9F5')` |
| Highlight row bg | `set_cell_shading(cell, 'F0EEE6')` |
| Positive emphasis | `run.font.color.rgb = AGENTMAN_500; run.font.bold = True` |
| Negative emphasis | `run.font.color.rgb = AGENTMAN_600; run.font.bold = True` |
| Badges | `set_cell_shading(cell, 'F6EAE6')` + `run.font.color.rgb = AGENTMAN_800` |
| Document metadata | `doc.core_properties.author` / `.title` |

The same 70/20/10 visual weight, terracotta budget (max 3 per section), and banned color rules apply to DOCX output identically to PDF.

## Migration from Previous Style

When updating from the previous agentman-styleguide-based approach:

| Previous Pattern | New Pattern (PPTX-style) |
|---|---|
| `AGENTMAN_800` (#703B2D) dark table header bg + white text | `AGENTMAN_100` (#F6EAE6) light fill + `AGENTMAN_500` (#CC785C) text |
| `SLATE_200` (#E2E8F0) table borders | `AGENTMAN_150` (#E3DACC) warm borders |
| `SUCCESS` (#10B981) green for positive data | `AGENTMAN_500` (#CC785C) terracotta for emphasis |
| `ERROR` (#EF4444) red for negative data | `AGENTMAN_600` (#A65945) deep terracotta for concern |
| `WARNING` (#F59E0B) amber for caution | `AGENTMAN_400` (#D97757) warm highlight |
| Green/amber/red badge left-borders | No colored borders — all badges use `AGENTMAN_200` border only |
| Colored verdict text (Buy green, Avoid red) | Terracotta-family: "Buy" `AGENTMAN_500`, "Avoid" `AGENTMAN_600` |
| Semantic colors as inline text | Terracotta-family emphasis, or ✓/✗ symbols for comparison |
