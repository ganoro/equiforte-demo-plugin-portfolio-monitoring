---
description: "Use this skill any time a .pptx file is involved — as input, output, or both. Includes creating slide decks, reading/parsing .pptx files, editing existing presentations, working with templates. Also generates PE/VC presentations with consistent formatting, charts, and tables. Always read the design-system skill first for PE/VC outputs."
---

# PPTX Generator

## Quick Reference

| Task | Guide |
|------|-------|
| Read/analyze content | `python -m markitdown presentation.pptx` |
| Edit or create from template | Read [editing.md](editing.md) |
| Create from scratch | Read [pptxgenjs.md](pptxgenjs.md) |

## Reading Content

```bash
# Text extraction
python -m markitdown presentation.pptx

# Visual overview (slide thumbnails)
python scripts/thumbnail.py presentation.pptx

# Raw XML access
python scripts/office/unpack.py presentation.pptx unpacked/
```

## Editing Workflow

**Read [editing.md](editing.md) for full details.**

1. Analyze template with `scripts/thumbnail.py`
2. Unpack → manipulate slides → edit content → clean → pack

## Creating from Scratch

**Read [pptxgenjs.md](pptxgenjs.md) for full details.**

Use PptxGenJS when no template or reference presentation is available.

## Report Generation

**Before generating reports, read the design system files:**
- `/shared/plugins/support-7715ceab/skills/design-system/references/tokens.md` — colors, typography, spacing
- `/shared/plugins/support-7715ceab/skills/design-system/references/components.md` — component patterns
- `/shared/plugins/support-7715ceab/skills/design-system/references/language.md` — terminology, disclaimers
- `/shared/plugins/support-7715ceab/brand/assets/brand-overrides.json` — firm name, confidentiality notice

### Step 1 — Gather Content

Before generating, ensure all content is ready:

- Report data in `_research/` markdown files
- Slide structure defined
- All data tables populated with actual values (no placeholders)

### Step 2 — Write Python Script

Build a Python script using `python-pptx`. Pull all values from design system tokens.

```python
import os, shutil
from pptx import Presentation
from pptx.util import Inches, Pt, Emu
from pptx.dml.color import RGBColor
from pptx.enum.text import PP_ALIGN

# ── Design Tokens (from design-system/references/tokens.md) ──
PRIMARY      = RGBColor(0x1B, 0x3A, 0x5C)
ACCENT       = RGBColor(0x2E, 0x75, 0xB6)
TEXT         = RGBColor(0x2D, 0x2D, 0x2D)
TEXT_SEC     = RGBColor(0x66, 0x66, 0x66)
TEXT_INV     = RGBColor(0xFF, 0xFF, 0xFF)
SURFACE      = RGBColor(0xF7, 0xF8, 0xFA)
BORDER       = RGBColor(0xD9, 0xDE, 0xE3)
POSITIVE     = RGBColor(0x1A, 0x7A, 0x3A)
WARNING      = RGBColor(0xC6, 0x77, 0x00)
NEGATIVE     = RGBColor(0xC4, 0x26, 0x1D)
CRITICAL     = RGBColor(0x8B, 0x00, 0x00)

# Chart series colors (in order)
CHART_SERIES = [PRIMARY, ACCENT, RGBColor(0x5B,0x9B,0xD5), RGBColor(0xA5,0xC8,0xE1), POSITIVE, WARNING]

# ── Logo ──
LOGO_SRC = "/shared/plugins/support-7715ceab/brand/assets/logo.png"
LOGO_LOCAL = "logo.png"
if os.path.exists(LOGO_SRC):
    shutil.copy2(LOGO_SRC, LOGO_LOCAL)

def add_logo_to_slide(slide, left=Inches(0.5), top=Inches(0.3), width=Inches(1.5)):
    """Insert the firm logo onto a slide. Call on the title slide."""
    if os.path.exists(LOGO_LOCAL):
        slide.shapes.add_picture(LOGO_LOCAL, left, top, width=width)
```

### Step 3 — Execute and Verify

```bash
pip install python-pptx 2>/dev/null
python generate_pptx.py
ls -la output/report.pptx
```

Save output to `output/report.pptx`.

## QA (Required)

**Assume there are problems. Your job is to find them.**

### Content QA

```bash
python -m markitdown output.pptx
# Check for leftover placeholder text:
python -m markitdown output.pptx | grep -iE "xxxx|lorem|ipsum|this.*(page|slide).*layout"
```

### Visual QA

Convert slides to images, then inspect visually using a subagent:

```bash
python scripts/office/soffice.py --headless --convert-to pdf output.pptx
pdftoppm -jpeg -r 150 output.pdf slide
```

This creates `slide-01.jpg`, `slide-02.jpg`, etc. Inspect for overlapping elements, text overflow, spacing issues, low contrast.

### Verification Loop

1. Generate slides → Convert to images → Inspect
2. List issues found
3. Fix issues
4. Re-verify affected slides
5. Repeat until clean

## Converting to Images

```bash
python scripts/office/soffice.py --headless --convert-to pdf output.pptx
pdftoppm -jpeg -r 150 output.pdf slide
```

## Dependencies

- `pip install "markitdown[pptx]"` — text extraction
- `pip install Pillow` — thumbnail grids
- `npm install -g pptxgenjs` — creating from scratch
- LibreOffice (`soffice`) — PDF conversion (auto-configured via `scripts/office/soffice.py`)
- Poppler (`pdftoppm`) — PDF to images

## Slide Types

### Title Slide

Per design-system Title Page component:

- Blank layout (index 6), white background
- **Insert logo**: call `add_logo_to_slide(slide)` — places logo top-left, max 1.5 in wide
- Title: `primary`, 32pt Bold, centered
- Subtitle: `text-secondary`, 20pt
- Date and confidentiality at bottom

### Title Bar (Content Slides)

- Full-width rectangle at slide top, `primary` fill, 1.0 in tall
- Title text: `text-inverse`, 24pt Bold, left-aligned with 0.5 in padding

### Table Slide

Per design-system Data Table component:

- Title bar at top
- Table below, max 8–10 rows per slide
- Header row: `primary` fill, white Bold 10pt
- Alternating rows: white / `surface`
- Source/as-of note in footer area: `text-secondary`, 8pt

### Chart Slide

- Title bar at top
- Chart uses series colors from tokens
- White chart background, `border-light` horizontal grid lines only
- Legend below chart
- Axis labels: `text-secondary`, 9pt

### KPI Slide

Per design-system KPI Card component:

- 3–4 cards in a row with equal width, 0.15 in gap
- Card fill: `surface`, border: `border`
- Value: status-colored, 36pt Bold
- Label: `text-secondary`, 11pt, uppercase

## Formatting Standards

| Element | Font | Size | Color |
|---------|------|------|-------|
| Slide title | Calibri Bold | 24pt | `text-inverse` on `primary` bar |
| Body text | Calibri | 12pt | `text` |
| Table header | Calibri Bold | 10pt | `text-inverse` on `primary` |
| Table body | Calibri | 10pt | `text` |
| Footer | Calibri | 8pt | `text-secondary` |
| Positive values | Calibri | 10pt | `positive` |
| Negative values | Calibri | 10pt | `negative` |

## Slide Dimensions

- 16:9 widescreen: 13.333 × 7.5 in
- Safe margin: 0.5 in from all edges

## Important Notes

- Always include "CONFIDENTIAL" on title slide and in footer
- Include slide numbers bottom-right
- Include as-of date on every data slide
- Include source attribution on chart/table slides
- Max 25 slides for standard presentations
- Apply conditional coloring per design-system semantic tokens
