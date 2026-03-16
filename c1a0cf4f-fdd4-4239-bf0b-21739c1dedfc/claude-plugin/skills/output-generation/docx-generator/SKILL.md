---
description: "Use this skill whenever creating, reading, editing, or manipulating Word documents (.docx files). Triggers include: any mention of 'Word doc', '.docx', or requests to produce professional documents with tables of contents, headings, page numbers, tracked changes, or comments. Also generates PE/VC reports with consistent formatting, tables, headers, and footers. Always read the design-system skill first for PE/VC outputs."
---

# DOCX Generator

A .docx file is a ZIP archive containing XML files.

## Quick Reference

| Task | Approach |
|------|----------|
| Read/analyze content | `pandoc` or unpack for raw XML |
| Create new document | Use `docx-js` (`npm install -g docx`) — see Creating section below |
| Edit existing document | Unpack → edit XML → repack |

### Converting .doc to .docx

```bash
python scripts/office/soffice.py --headless --convert-to docx document.doc
```

### Reading Content

```bash
# Text extraction with tracked changes
pandoc --track-changes=all document.docx -o output.md

# Raw XML access
python scripts/office/unpack.py document.docx unpacked/
```

### Converting to Images

```bash
python scripts/office/soffice.py --headless --convert-to pdf document.docx
pdftoppm -jpeg -r 150 document.pdf page
```

### Accepting Tracked Changes

```bash
python scripts/accept_changes.py input.docx output.docx
```

## Creating New Documents

Generate .docx files with JavaScript (`npm install -g docx`), then validate:

```bash
python scripts/office/validate.py doc.docx
```

If validation fails, unpack, fix the XML, and repack.

### Critical Rules for docx-js

- **Set page size explicitly** — defaults to A4; use US Letter (12240 x 15840 DXA) for US documents
- **Landscape: pass portrait dimensions** — docx-js swaps width/height internally
- **Never use `\n`** — use separate Paragraph elements
- **Never use unicode bullets** — use `LevelFormat.BULLET` with numbering config
- **PageBreak must be in Paragraph** — standalone creates invalid XML
- **ImageRun requires `type`** — always specify png/jpg/etc
- **Always set table `width` with DXA** — never use `WidthType.PERCENTAGE` (breaks in Google Docs)
- **Tables need dual widths** — `columnWidths` array AND cell `width`, both must match
- **Use `ShadingType.CLEAR`** — never SOLID for table shading
- **Never use tables as dividers/rules** — use border on a Paragraph instead
- **TOC requires HeadingLevel only** — no custom styles on heading paragraphs

## Editing Existing Documents

**Follow all 3 steps in order.**

### Step 1: Unpack
```bash
python scripts/office/unpack.py document.docx unpacked/
```

### Step 2: Edit XML

Edit files in `unpacked/word/`. Use the Edit tool directly for string replacement — do not write Python scripts.

**Smart quotes:** Use XML entities for professional typography:
| Entity | Character |
|--------|-----------|
| `&#x2018;` | ' (left single) |
| `&#x2019;` | ' (right single / apostrophe) |
| `&#x201C;` | " (left double) |
| `&#x201D;` | " (right double) |

**Adding comments:**
```bash
python scripts/comment.py unpacked/ 0 "Comment text"
python scripts/comment.py unpacked/ 1 "Reply text" --parent 0
```

### Step 3: Pack
```bash
python scripts/office/pack.py unpacked/ output.docx --original document.docx
```

## PE/VC Report Generation

**Before generating PE/VC reports, read the design system files:**
- `/shared/plugins/{{PLUGIN_NAME}}/skills/design-system/references/tokens.md` — colors, typography, spacing
- `/shared/plugins/{{PLUGIN_NAME}}/skills/design-system/references/components.md` — component patterns
- `/shared/plugins/{{PLUGIN_NAME}}/skills/design-system/references/language.md` — terminology, disclaimers
- `/shared/plugins/{{PLUGIN_NAME}}/brand/assets/brand-overrides.json` — firm name, confidentiality notice

Copy the logo into the workspace: `cp /shared/plugins/{{PLUGIN_NAME}}/brand/assets/logo.png ./logo.png 2>/dev/null || true`

### Step 1 — Gather Content

Ensure all report content is finalized in `_research/` markdown files before generating.

### Step 2 — Write Python Script

Build a Python script that uses `python-docx`. Pull all color values, font sizes, and spacing from the design system tokens — do not hardcode.

```python
import os, shutil
from docx import Document
from docx.shared import Inches, Pt, RGBColor
from docx.enum.text import WD_ALIGN_PARAGRAPH
from docx.enum.table import WD_TABLE_ALIGNMENT

# ── Design Tokens (from design-system/references/tokens.md) ──
PRIMARY     = RGBColor(0x1B, 0x3A, 0x5C)
ACCENT      = RGBColor(0x2E, 0x75, 0xB6)
TEXT        = RGBColor(0x2D, 0x2D, 0x2D)
TEXT_SEC    = RGBColor(0x66, 0x66, 0x66)
TEXT_INV    = RGBColor(0xFF, 0xFF, 0xFF)
SURFACE     = RGBColor(0xF7, 0xF8, 0xFA)
POSITIVE    = RGBColor(0x1A, 0x7A, 0x3A)
WARNING     = RGBColor(0xC6, 0x77, 0x00)
NEGATIVE    = RGBColor(0xC4, 0x26, 0x1D)
CRITICAL    = RGBColor(0x8B, 0x00, 0x00)

# ── Logo ──
LOGO_SRC = "/shared/plugins/{{PLUGIN_NAME}}/brand/assets/logo.png"
LOGO_LOCAL = "logo.png"
if os.path.exists(LOGO_SRC):
    shutil.copy2(LOGO_SRC, LOGO_LOCAL)

def add_logo_to_doc(doc, width=Inches(2.0)):
    """Insert the firm logo at the current position in the document."""
    if os.path.exists(LOGO_LOCAL):
        doc.add_picture(LOGO_LOCAL, width=width)
```

### Step 3 — Execute and Verify

```bash
pip install python-docx 2>/dev/null
python generate_docx.py
ls -la output/report.docx
```

Save output to `output/report.docx`.

## Dependencies

- **pandoc** — text extraction
- **docx** — `npm install -g docx` (new documents)
- **LibreOffice** — PDF conversion (auto-configured via `scripts/office/soffice.py`)
- **Poppler** — `pdftoppm` for images

## Document Structure

### Page Setup

- Letter size (8.5 × 11 in)
- Margins: Top 1.0 in, Bottom 1.0 in, Left 1.25 in, Right 1.0 in
- Font: Calibri throughout

### Required Sections

1. **Title page** — call `add_logo_to_doc(doc)` first, then add title, subtitle, date, and "CONFIDENTIAL"
2. **Table of contents** — placeholder with update-field instruction
3. **Report body** — sections with H1/H2/H3 hierarchy per tokens
4. **Disclaimers** — standard disclaimer text from `references/language.md`

### Headers and Footers

- Header: Fund name (left), "CONFIDENTIAL" (right), 8pt, `text-secondary`
- Footer: "Page X of Y" (center), report date (right), 8pt
- Thin rule separating header/footer from content

### Table Formatting

Follow the Data Table component pattern:

- Header row: `primary` fill, white Bold 10pt text
- Alternating rows: white / `surface`
- Right-align numeric columns
- Total rows: Bold with `border-strong` top border
- Source footnote below: `text-secondary`, 8pt

### Number Formatting

Per tokens.md:

- Currency: $X,XXX or $X.XM
- Percentages: X.X%
- Multiples: X.XXx
- Negative: (X,XXX) in `negative` color

## Important Notes

- Always include confidentiality notice in header
- Always include as-of date on title page
- Include source citations for all data tables
- Label all figures as audited or unaudited
- Include standard disclaimers at end (see `references/language.md`)
- Apply confidence labels per language guide (VERIFIED/REPORTED/ESTIMATED/ASSUMED)
