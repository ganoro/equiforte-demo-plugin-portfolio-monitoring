# Brand Configuration — Equiforte

This directory holds Equiforte brand assets. These customize the look and language of all generated reports.

## Assets

Place brand files in `assets/`:

| File | Purpose | Format |
|------|---------|--------|
| `logo.png` | Equiforte blue wordmark for report headers and title pages | PNG, transparent background, min 300px wide |
| `logo-dark.png` | Logo variant for dark backgrounds (optional) | PNG, transparent background |
| `logo-sq.png` | Square icon for footers and watermarks (optional) | PNG, 64x64px or 128x128px |

## Brand Colors

Equiforte's primary brand color is **#3563AC** (the bold blue from the wordmark logo).

## Customization

The `brand-overrides.json` file in `assets/` controls firm name, colors, and legal notices:

```json
{
  "firm_name": "Equiforte",
  "firm_name_short": "Equiforte",
  "tagline": "AI-Powered Private Equity Intelligence",
  "colors": {
    "primary": "#3563AC",
    "accent": "#3563AC"
  },
  "confidentiality_notice": "CONFIDENTIAL — Equiforte — For Authorized Recipients Only",
  "disclaimer": "..."
}
```

The design system skill reads these overrides and applies them to all generated output.
