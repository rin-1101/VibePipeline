# 4. Design Brief

This document defines the visual identity and UI rules that keep the web app's colors, fonts, layouts, and branding consistent.

**Project:** [App name]  
**Status:** [Draft / Agreed / Revised]  
**Owner:** [Name or role]  
**Last updated:** [YYYY-MM-DD]

## Brand direction

- **App or brand name:** [Name]
- **Audience:** [Users from the product requirements]
- **Personality:** [For example: calm, practical, or playful]
- **Desired experience:** [How using the app should feel]
- **Brand assets:** [Logo, icons, imagery, and asset locations]
- **Voice:** [Tone for labels, guidance, confirmations, and errors]

## Color palette

Specify exact color values and where each color is used.

| Color role | Value | Usage |
| --- | --- | --- |
| Primary | [HEX or other value] | [Main actions and brand elements] |
| Secondary | [Value] | [Supporting elements] |
| Background | [Value] | [Page background] |
| Surface | [Value] | [Cards, panels, and dialogs] |
| Primary text | [Value] | [Main content] |
| Muted text | [Value] | [Supporting content] |
| Border | [Value] | [Separators and outlines] |
| Success / warning / error | [Values] | [Status feedback] |

Define hover, focus, selected, and disabled states. If multiple themes are supported, document their corresponding values.

## Typography

| Text role | Font and fallback | Size | Weight | Line height |
| --- | --- | --- | --- | --- |
| Page heading | [Font stack] | [Size] | [Weight] | [Line height] |
| Section heading | [Font stack] | [Size] | [Weight] | [Line height] |
| Body | [Font stack] | [Size] | [Weight] | [Line height] |
| Label and helper text | [Font stack] | [Size] | [Weight] | [Line height] |

State how fonts are loaded and whether their licensing permits the intended use.

## Layout and spacing

Define content widths, grids, spacing increments, alignment, border radii, shadows, and content density. Specify mobile, tablet, and desktop behavior, including navigation changes and overflow handling for forms and tables.

## Shared components

| Component | Appearance and variants | Interaction states | Usage rules |
| --- | --- | --- | --- |
| Buttons | [Primary, secondary, and other needed variants] | [Hover, focus, disabled, loading] | [When to use each] |
| Inputs | [Labels, borders, and helper text] | [Focus, invalid, disabled] | [Validation placement] |
| Navigation | [Menus or tabs] | [Active and focus] | [Selection rules] |
| Cards and tables | [Spacing and hierarchy] | [Empty, loading, selected] | [Content rules] |
| Alerts and dialogs | [Status appearance] | [Open, close, focus] | [Feedback rules] |

## Accessibility and consistent branding

Specify readable contrast, visible keyboard focus, accessible labels, and status cues that do not rely only on color. Define motion behavior and reduced-motion support if animation is used.

Use the same logo treatment, palette, typography, spacing, component styles, terminology, and tone across every page. Describe permitted exceptions and the reason for each.

## Page references and assets

Link wireframes or mockups to the page IDs in [App Flow](app-flow.md). Record asset locations, usage rights, and reusable design tokens so developers can implement the brief consistently.

## Completion criteria

This document is ready when a developer can reproduce the main pages and shared components using documented visual rules, including responsive and accessible interaction states.
