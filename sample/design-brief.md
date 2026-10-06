# 4. Design Brief: MarketLens AI

**Status:** Proposed sample specification  
**Owner:** Product designer  
**Last updated:** 2026-10-06

## Brand direction

MarketLens AI should feel calm, analytical, and readable. Its audience needs to compare evidence, dates, and uncertainty without visual pressure to act on a prediction.

Use a text wordmark, **MarketLens AI**, with a simple lens-and-line icon created as SVG during implementation. Avoid animation suggesting that a forecast is live market data. Interface language uses “forecast,” “estimate,” and “historical evaluation.”

## Colors

| Token | Value | Purpose |
| --- | --- | --- |
| `--brand` | `#0F766E` | Primary buttons and active navigation. |
| `--brand-hover` | `#115E59` | Hover and pressed primary actions. |
| `--header` | `#0F172A` | Header background. |
| `--background` | `#F8FAFC` | Main page background. |
| `--surface` | `#FFFFFF` | Cards, forms, and panels. |
| `--text` | `#0F172A` | Main text. |
| `--muted` | `#475569` | Secondary text. |
| `--border` | `#CBD5E1` | Decorative card separators. |
| `--control-border` | `#64748B` | Input boundaries. |
| `--forecast` | `#6D28D9` | Forecast markers and dashed connectors. |
| `--success` | `#166534` | Positive status text with explicit label. |
| `--warning` | `#92400E` | Stale-data and caution text. |
| `--error` | `#B91C1C` | Errors and negative status text. |
| `--focus` | `#1D4ED8` | Keyboard focus outline. |

Use white text on dark headers and primary buttons. Disabled controls use reduced emphasis plus the actual disabled state; color alone does not communicate status. Verify final color combinations for WCAG AA contrast during implementation, including translucent chart bands.

## Typography

Use system fonts to avoid an external font dependency: `Segoe UI, Roboto, Helvetica, Arial, sans-serif`. Use `ui-monospace, Consolas, monospace` for model versions and technical IDs.

| Role | Size | Weight | Line height |
| --- | --- | --- | --- |
| Page heading | 32px desktop; 26px mobile | 700 | 1.2 |
| Section heading | 22px | 600 | 1.3 |
| Body and inputs | 16px | 400 | 1.5 |
| Labels and table text | 14px | 500 | 1.4 |
| Forecast headline value | 32px | 700 | 1.2 |

Use tabular numerals for aligned values. Show USD prices to two decimal places and percentage returns to two decimal places; preserve full precision in stored calculations. Display session dates as `YYYY-MM-DD` and label timestamps with their timezone.

## Layout and spacing

Use a maximum content width of 1200px, centered with 24px desktop and 16px mobile padding. Use spacing steps of 4, 8, 12, 16, 24, and 32px; cards have 12px corner radii and subtle shadows.

- **Below 640px:** One column, collapsed navigation, full-width actions, forecast summary above the chart.
- **640-1023px:** Two-column summary cards with full-width charts.
- **1024px and above:** Main content plus a supporting stock summary panel.

Tables may scroll horizontally inside their own labeled regions. The overall page must not overflow horizontally at 360px width.

## Shared components

| Component | Visual and behavior rules |
| --- | --- |
| Primary button | Teal fill, white label, 44px minimum height; spinner and descriptive loading label. |
| Secondary button | White background, dark text, visible border; same dimensions. |
| Search field | Persistent label, clear action, keyboard-operable suggestions. |
| Horizon selector | Two options: 1 trading session and 5 trading sessions; selected state uses text and styling. |
| Metric card | Label, value, units, and supporting date or basis; no unexplained confidence score. |
| Status badge | Text plus icon for Fresh, Stale, Demo data, Running, Failed, and Unavailable. |
| Error panel | Plain explanation and a clear next action; no raw stack traces. |
| Job table | Status, timestamps, and permitted actions; completed rows remain inspectable. |

## Charts and uncertainty

Historical observations use a solid navy line. The forecast endpoint uses a purple marker with a dashed guide from the cutoff. A labeled shaded interval or error bar marks the estimated 10th-90th percentile range at the target session.

Include axes, units, legend, data source, and cutoff. Tooltips distinguish observed adjusted prices from forecasts. Do not connect two horizon forecasts as if they were a daily projected path. Positive and negative returns also include `+` and `-` signs and words where helpful.

Provide a keyboard-accessible table of chart values and a text summary of the forecast. Explain that the interval is nominal and link its measured historical coverage.

## Branding and accessibility

Use the same header, typography, palette, terminology, and spacing on P-01 through P-07. The mobile layout retains forecast dates and uncertainty rather than hiding them.

Use semantic headings, visible focus, associated form labels, accessible chart summaries, and polite announcements for asynchronous results. Honor reduced-motion preferences; no essential information depends on animation or color. Target [WCAG 2.2 AA](https://www.w3.org/TR/WCAG22/) and record accessibility checks in the implementation plan.

No final mockups, logo files, or verified contrast report exist yet. T-04 produces reusable design tokens and T-11 verifies the resulting UI against this brief.
