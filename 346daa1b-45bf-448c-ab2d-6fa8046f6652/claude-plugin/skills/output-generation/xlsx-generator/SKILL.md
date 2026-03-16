---
description: "Use this skill any time a spreadsheet file is the primary input or output — .xlsx, .xlsm, .csv, or .tsv files. Includes creating, reading, editing, formatting, charting, and fixing spreadsheets. Also generates PE/VC financial workbooks with fund performance, portfolio data, cash flows, and waterfall calculations. Always read the design-system skill first for PE/VC outputs."
---

# XLSX Generator

## Requirements for All Excel Files

- Use a consistent, professional font (e.g., Calibri, Arial)
- Every Excel model MUST be delivered with ZERO formula errors (#REF!, #DIV/0!, #VALUE!, #N/A, #NAME?)
- When updating existing templates, EXACTLY match existing format and conventions

## CRITICAL: Use Formulas, Not Hardcoded Values

Always use Excel formulas instead of calculating values in Python and hardcoding them:

```python
# ❌ WRONG
total = df['Sales'].sum()
sheet['B10'] = total

# ✅ CORRECT
sheet['B10'] = '=SUM(B2:B9)'
```

## Common Workflow

1. **Choose tool**: pandas for data, openpyxl for formulas/formatting
2. **Create/Load**: Create new workbook or load existing file
3. **Modify**: Add/edit data, formulas, and formatting
4. **Save**: Write to file
5. **Recalculate formulas (MANDATORY)**: `python scripts/recalc.py output.xlsx`
6. **Verify and fix errors**: Check JSON output for error details

The `scripts/recalc.py` script:
- Automatically sets up LibreOffice macro on first run
- Recalculates all formulas in all sheets
- Scans ALL cells for Excel errors
- Returns JSON with detailed error locations and counts
- Works on both Linux and macOS

## Financial Models Color Coding

- **Blue text** (0,0,255): Hardcoded inputs
- **Black text** (0,0,0): ALL formulas and calculations
- **Green text** (0,128,0): Links from other worksheets
- **Red text** (255,0,0): External links to other files
- **Yellow background** (255,255,0): Key assumptions needing attention

## Number Formatting Standards

- **Years**: Format as text strings ("2024" not "2,024")
- **Currency**: `$#,##0` format; ALWAYS specify units in headers ("Revenue ($mm)")
- **Zeros**: Format to display as "-" (e.g., `$#,##0;($#,##0);-`)
- **Percentages**: Default to `0.0%`
- **Multiples**: Format as `0.0x`
- **Negative numbers**: Use parentheses `(123)` not minus `-123`

## PE/VC Report Generation

**Before generating PE/VC reports, read the design system files:**
- `/shared/plugins/{{PLUGIN_NAME}}/skills/design-system/references/tokens.md` — colors, typography, number formatting
- `/shared/plugins/{{PLUGIN_NAME}}/skills/design-system/references/components.md` — table patterns, conditional formatting
- `/shared/plugins/{{PLUGIN_NAME}}/brand/assets/brand-overrides.json` — firm name, confidentiality notice

### Step 1 — Gather Data

Collect all numerical data from `_research/` computation results. Excel outputs should contain the underlying data that supports reports and presentations.

### Step 2 — Write Python Script

Build a Python script using `openpyxl`. Pull all values from design system tokens.

```python
import os, shutil
from openpyxl import Workbook
from openpyxl.drawing.image import Image as XlImage
from openpyxl.styles import Font, PatternFill, Alignment, Border, Side, numbers
from openpyxl.chart import BarChart, LineChart, Reference
from openpyxl.utils import get_column_letter

# ── Design Tokens (from design-system/references/tokens.md) ──
HEADER_FILL    = PatternFill(start_color='1B3A5C', end_color='1B3A5C', fill_type='solid')
SURFACE_FILL   = PatternFill(start_color='F7F8FA', end_color='F7F8FA', fill_type='solid')
POSITIVE_FILL  = PatternFill(start_color='E8F5EC', end_color='E8F5EC', fill_type='solid')
WARNING_FILL   = PatternFill(start_color='FFF3D6', end_color='FFF3D6', fill_type='solid')
NEGATIVE_FILL  = PatternFill(start_color='FDECEA', end_color='FDECEA', fill_type='solid')
CRITICAL_FILL  = PatternFill(start_color='F5E0E0', end_color='F5E0E0', fill_type='solid')

HEADER_FONT    = Font(name='Calibri', size=10, bold=True, color='FFFFFF')
DATA_FONT      = Font(name='Calibri', size=10, color='2D2D2D')
POSITIVE_FONT  = Font(name='Calibri', size=10, color='1A7A3A')
WARNING_FONT   = Font(name='Calibri', size=10, color='C67700')
NEGATIVE_FONT  = Font(name='Calibri', size=10, color='C4261D')
CRITICAL_FONT  = Font(name='Calibri', size=10, color='8B0000')
CAPTION_FONT   = Font(name='Calibri', size=8, color='666666')

BORDER_LIGHT   = Border(bottom=Side(style='thin', color='E8ECF0'))
BORDER_STRONG  = Border(bottom=Side(style='thin', color='B0B8C1'))
TAB_COLOR      = '2E75B6'  # accent

# ── Logo ──
LOGO_SRC = "/shared/plugins/{{PLUGIN_NAME}}/brand/assets/logo.png"
LOGO_LOCAL = "logo.png"
if os.path.exists(LOGO_SRC):
    shutil.copy2(LOGO_SRC, LOGO_LOCAL)

def add_cover_sheet(wb, title, subtitle, as_of_date):
    """Create a Cover tab as the first sheet with logo, title, and date."""
    ws = wb.active
    ws.title = "Cover"
    ws.sheet_properties.tabColor = '1B3A5C'
    # Insert logo at cell A1
    if os.path.exists(LOGO_LOCAL):
        img = XlImage(LOGO_LOCAL)
        img.width = 200   # pixels
        img.height = int(img.height * (200 / img.width))  # maintain aspect ratio
        ws.add_image(img, "A1")
    # Title in row 8 (below logo)
    ws.merge_cells("A8:F8")
    cell = ws["A8"]
    cell.value = title
    cell.font = Font(name='Calibri', size=22, bold=True, color='1B3A5C')
    cell.alignment = Alignment(horizontal='left')
    # Subtitle
    ws.merge_cells("A9:F9")
    cell = ws["A9"]
    cell.value = subtitle
    cell.font = Font(name='Calibri', size=14, color='666666')
    # Date
    ws.merge_cells("A10:F10")
    cell = ws["A10"]
    cell.value = f"As of {as_of_date}"
    cell.font = Font(name='Calibri', size=11, color='666666')
    # Confidentiality
    ws.merge_cells("A12:F12")
    cell = ws["A12"]
    cell.value = "CONFIDENTIAL"
    cell.font = Font(name='Calibri', size=10, color='999999')
    # Column width
    ws.column_dimensions['A'].width = 35
```

### Step 3 — Execute and Verify

```bash
pip install openpyxl 2>/dev/null
python generate_xlsx.py
ls -la output/report.xlsx
# MANDATORY: Recalculate formulas
python scripts/recalc.py output/report.xlsx
```

Save output to `output/report.xlsx`.

## Standard Tab Structure

### Cover Tab (REQUIRED — must be the first tab)

Call `add_cover_sheet(wb, title, subtitle, as_of_date)` immediately after creating the workbook. This inserts the firm logo, report title, and confidentiality notice as the first tab.

### Fund Summary Tab

| Field | Value |
|-------|-------|
| Fund Name | |
| Vintage Year | |
| Fund Size | |
| Currency | |
| Net IRR | |
| TVPI / DPI / RVPI | |
| Total Called | |
| Total Distributed | |
| Current NAV | |
| Unfunded | |

### Portfolio Tab

| Company | Sector | Entry Date | Cost | Fair Value | MOIC | % NAV | Revenue | EBITDA | Status |
|---------|--------|-----------|------|------------|------|-------|---------|--------|--------|

### Cash Flows Tab

| Date | Type | Description | Amount | Cumulative |
|------|------|-------------|--------|------------|

### Performance Tab (Quarterly)

| Quarter | NAV | Contributions | Distributions | Net IRR | TVPI | DPI | RVPI |
|---------|-----|--------------|---------------|---------|------|-----|------|

### Sources & Notes Tab (Required)

Include data provenance, confidence labels, and assumptions for every key figure.

## Formatting Rules

### Number Formats (from tokens.md)

| Data Type | Cell Format | Example |
|-----------|------------|---------|
| Currency | `$#,##0` | $1,234,567 |
| Currency (M) | `$#,##0.0,,"M"` | $12.3M |
| Percentage | `0.0%` | 15.2% |
| Multiple | `0.00"x"` | 1.85x |
| Date | `YYYY-MM-DD` | 2024-09-30 |
| Negative currency | `$#,##0;[Red]($#,##0)` | ($1,234) |

### Table Formatting (from components.md)

- Header row: `HEADER_FILL` + `HEADER_FONT`, center-aligned
- Odd rows: white background
- Even rows: `SURFACE_FILL`
- Total rows: Bold, `BORDER_STRONG` top
- Right-align all numeric columns
- Freeze pane at A2
- Auto-filter on header row

### Conditional Formatting

Apply to status and performance columns:

| Condition | Font | Fill |
|-----------|------|------|
| Positive / above target | `POSITIVE_FONT` | `POSITIVE_FILL` |
| Warning / approaching | `WARNING_FONT` | `WARNING_FILL` |
| Negative / below target | `NEGATIVE_FONT` | `NEGATIVE_FILL` |
| Critical / write-off | `CRITICAL_FONT` | `CRITICAL_FILL` |

### Column Widths

| Column type | Width (chars) |
|-------------|---------------|
| Label / name | 25–30 |
| Currency | 15 |
| Percentage | 10 |
| Date | 12 |
| Multiple | 10 |

## Important Notes

- Include formulas where possible (not static values) so users can adjust
- Use TVPI = DPI + RVPI as a formula cross-check
- Include data validation notes in cell comments
- Protect formula cells from accidental editing (no password)
- Tab color: `accent` (`2E75B6`) on all worksheets
- Set print area and page breaks for each tab
- Print header: fund name left, "CONFIDENTIAL" right
