---
name: ui-design-principles
description: >
  Rules for visual hierarchy, whitespace, spacing scales, layout, depth (shadows, elevation),
  and polish. Apply whenever writing or reviewing CSS/HTML styles, deciding on padding/margin/gap
  values, choosing shadow levels, structuring page layouts, handling responsive design, or
  improving the overall look and feel of a UI.
  NOT for picking specific colors (use ui-design:color-palettes), fonts (use ui-design:font-recommendations),
  building specific components (use ui-design:component-gallery), or accessibility/WCAG compliance
  (use ui-design:wcag-2.2).
---

# UI Design Principles

## Starting from Scratch

### Start with a Feature, Not a Layout
- Don't begin with the shell (navbar, sidebar, footer). Start with the actual feature/functionality.
- Design in grayscale first to force clear hierarchy through spacing, contrast, and size rather than color.
- Don't design every single feature upfront. Work in short cycles: design a simple version, implement it, iterate.

### Choose a Personality
- Font choice affects personality: serif = elegant/classic, rounded sans-serif = playful, neutral sans-serif = professional.
- Color affects personality: blue = safe/familiar, gold = high-end, pink = fun/playful.
- Border radius affects personality: small = neutral/serious, large = playful, none = formal.

### Limit Your Choices
- Define systems in advance: spacing scales, font sizes, colors, shadows, etc.
- Systematize everything to avoid decision fatigue and inconsistency.

## Hierarchy is Everything

### Size Isn't Everything
- Don't rely on font size alone for hierarchy. Use font weight and color as primary tools.
- For primary content: use dark color (e.g., hsl(210, 15%, 20%)), normal-to-bold weight.
- For secondary content: use medium grey (e.g., hsl(210, 10%, 55%)), normal weight.
- For tertiary content: use lighter grey (e.g., hsl(210, 10%, 70%)), normal weight, smaller size.
- Use 2-3 shades of grey for text: dark, medium, and light. Avoid more than that.
- Don't use grey text on colored backgrounds. Instead, use the background color with adjusted opacity or a hand-picked color that matches.

### Emphasize by De-emphasizing
- Sometimes the best way to make something stand out is to de-emphasize the things around it.
- Instead of making a primary action bigger, make secondary actions smaller/lighter.

### Labels Are a Last Resort
- Don't slap a label on everything. The data itself often indicates what it represents.
- Combine labels with values when possible (e.g., "12 left in stock" instead of "In Stock: 12").
- When you do use labels, de-emphasize them (smaller, lighter, uppercase) and emphasize the value.

### Separate Visual Hierarchy from Document Hierarchy
- Don't let semantic HTML dictate visual styling. An h3 can be visually large and bold when it's the page title.
- Style based on the role content plays in the UI, not its HTML tag.

### Balance Weight and Contrast
- Bold text with low contrast can have the same visual weight as normal text with high contrast.
- Icons beside text often feel too heavy; reduce contrast/opacity on the icon to balance.

### Semantics Are Secondary
- Use semantic colors (red for destructive actions) as secondary indicators, not primary ones.
- For destructive actions: make the button smaller/less prominent, not big and red.

## Layout and Spacing

### Start with Too Much White Space
- Begin with way more space than you think you need, then reduce.
- White space should be removed, not added.

### Establish a Spacing and Sizing System
- Use a constrained scale based on a base value of 16px:
  - 4px, 8px, 12px, 16px, 24px, 32px, 48px, 64px, 96px, 128px, 192px, 256px, 384px, 512px, 640px, 768px
- Each step should be at least 25% different from adjacent values.
- A linear scale (multiples of 4px) doesn't work because jumps feel too small at large sizes and too large at small sizes.

### You Don't Have to Fill the Whole Screen
- If content needs 600px, use 600px. Don't spread it to fill 1400px.
- Not everything needs to be full-width. A login form on a wide page should still be constrained.
- Start with mobile (~400px) and work up.
- Use columns instead of stretching narrow content.

### Grids Are Overrated
- Don't make everything fluid/percentage-based. Sidebars should often have fixed widths.
- Give components the space they need. Use max-width instead of grid column widths.
- Don't shrink elements until you need to (responsive breakpoints).

### Relative Sizing Doesn't Scale
- Don't assume all elements should scale proportionally across screen sizes.
- Large elements shrink faster than small ones on smaller screens.
- Button padding should not be proportional to font size — larger buttons get more generous padding.

### Avoid Ambiguous Spacing
- When groups of elements lack visible separators, use spacing to show relationships.
- The space between a label and its input should be less than the space between form groups.
- More space around groups than within them. This applies to form fields, headings, list items, and horizontal layouts.

## Typography

### Establish a Type Scale
- Recommended scale: 12px, 14px, 16px, 18px, 20px, 24px, 30px, 36px, 48px, 60px, 72px.
- Don't use em units for type scales — use px or rem to guarantee consistency.
- Avoid modular scales (mathematical ratios) for interfaces — they produce fractional values and too few useful sizes.

### Use Good Fonts
- For UI design, default to neutral sans-serif fonts.
- System font stack: `-apple-system, Segoe UI, Roboto, Noto Sans, Ubuntu, Cantarell, Helvetica Neue`
- Filter fonts by number of weights: only consider typefaces with 5+ weights (10+ styles including italics).
- Optimize for legibility: avoid condensed typefaces with short x-heights for body text.
- Trust popular fonts: sort by popularity in font directories.

### Line Length
- Keep paragraphs 45-75 characters per line (20-35em).
- Use `max-width` in em units to control line length independent of container width.
- Wider content areas can contain images/components at full width while constraining paragraph text.

### Baseline Alignment
- When mixing font sizes on the same line, align by baseline, not center.
- `align-items: baseline;` not `align-items: center;`

### Line-Height Is Proportional
- Line-height and font size are inversely proportional.
- Small text (body): line-height 1.5-1.75
- Large text (headlines): line-height 1-1.25
- Wide content needs taller line-height; narrow content can use shorter line-height.

### Links
- Not every link needs a bright color. In link-heavy UIs, use bolder weight or darker color instead.
- Ancillary links can be styled on hover only.

### Text Alignment
- Default to left-aligned text for English.
- Center alignment works for headlines and short blocks (2-3 lines max).
- Right-align numbers in tables for easy comparison.
- Enable `hyphens: auto` when using justified text.

### Letter-Spacing
- Trust the typeface designer by default.
- Tighten letter-spacing for headlines using wide-spaced font families (`letter-spacing: -0.02em`).
- Increase letter-spacing for ALL CAPS text (`letter-spacing: 0.05em`).

## Working with Color

### Use HSL, Not Hex
- HSL represents colors as humans perceive them: hue (0-360 degrees), saturation (0-100%), lightness (0-100%).
- HSL makes it easy to create color variations by adjusting a single parameter.

### You Need More Colors Than You Think
- A real UI needs 8-10 shades per color, not just 5 hex codes.
- Three categories: Greys (8-10 shades), Primary colors (5-10 shades each), Accent colors (5-10 shades each for semantic states).
- True black looks unnatural. Start with a very dark grey.

### Define Shades Up Front
- Don't use CSS preprocessor functions (lighten/darken) to create shades on the fly.
- Pick a base color (good for a button background), then find the darkest shade (for text) and lightest shade (for tinted backgrounds).
- Fill in gaps: use 9 shades (100-900 scale). Start with 100, 500, 900, then fill 300, 700, then 200, 400, 600, 800.

### Saturation and Lightness
- As lightness approaches 0% or 100%, increase saturation to compensate for washed-out appearance.
- To make a color lighter without losing intensity, rotate hue toward bright hues (60°/yellow, 180°/cyan, 300°/magenta).
- To make a color darker, rotate hue toward dark hues (0°/red, 120°/green, 240°/blue).
- Don't rotate more than 20-30° or the color will look completely different.

### Grey Temperature
- Saturate greys with blue for a cool feel, or yellow/orange for a warm feel.
- Increase saturation for lighter and darker grey shades to maintain consistent temperature.

### Accessibility
- WCAG: 4.5:1 contrast ratio for normal text, 3:1 for large text.
- Use dark text on light colored backgrounds (flip contrast) instead of light text on dark colored backgrounds when possible.
- Rotate hue toward brighter colors to increase contrast on dark backgrounds without going pure white.
- Don't rely on color alone — use icons, text, or patterns to supplement color meaning (colorblindness).

## Creating Depth

### Emulate a Light Source
- Light comes from above. Top edges of raised elements are lighter; bottom edges are darker.
- Raised elements: lighter top border/inset shadow + small dark drop shadow below.
  ```css
  box-shadow: inset 0 1px 0 hsl(224, 84%, 74%);  /* top highlight */
  box-shadow: 0 1px 3px 0 hsla(0, 0%, 0%, .2);   /* drop shadow */
  ```
- Inset elements: darker top inset shadow + lighter bottom edge.
  ```css
  box-shadow: inset 0 2px 2px hsla(0, 0%, 0%, 0.1);  /* top shadow */
  ```

### Shadows Convey Elevation
- Small shadows = slightly raised (buttons): `box-shadow: 0 1px 3px hsla(0,0%,0%,.2)`
- Medium shadows = floating (dropdowns): `box-shadow: 0 4px 6px hsla(0,0%,0%,.1)`
- Large shadows = prominent (modals): `box-shadow: 0 15px 35px hsla(0,0%,0%,.2)`
- Define 5 shadow levels and stick to them.
- Use shadow changes for interactions: larger on hover/drag, smaller on click.

### Two-Part Shadows
- Combine a larger soft shadow (direct light) with a smaller tight shadow (ambient light).
- At higher elevations, the tight ambient shadow should become more subtle.

### Flat Design Depth
- Use lighter colors for raised elements, darker for recessed.
- Solid shadows (no blur): `box-shadow: 0 3px 0 hsl(220, 7%, 83%)`

### Overlap Elements
- Offset cards across background transitions to create layers.
- Use "invisible borders" (matching background color) between overlapping images.

## Working with Images

### Use Good Photos
- Bad photos ruin a design regardless of everything else. Use professional photography or high-quality stock.

### Text Over Images
- Add a semi-transparent dark overlay: `background-color: rgba(0, 0, 0, .5)`
- Lower image contrast and adjust brightness.
- Colorize: desaturate + solid fill with multiply blend mode.
- Add text shadow with large blur, no offset for subtle glow effect.

### Scaling
- Don't scale up icons designed for 16-24px. Enclose small icons in colored shapes instead.
- Don't scale down screenshots. Use tablet-size screenshots or partial screenshots.
- Redraw simplified versions of logos for small sizes (favicons).

### User-Uploaded Content
- Use fixed containers with `background-size: cover` to control aspect ratios.
- Prevent background bleed with subtle inner box shadow: `box-shadow: inset 0 0 0 1px hsla(0,0%,0%,.1)`

## Finishing Touches

### Supercharge Defaults
- Replace bullet points with icons (checkmarks, arrows, padlocks).
- Promote quotation marks to visual elements (larger, colored).
- Use custom checkboxes and radio buttons with brand colors.

### Accent Borders
- Add colored borders to: top of cards, active navigation items, side of alerts, under headlines, top of entire layouts.
- No graphic design talent needed — a colored rectangle adds significant polish.

### Decorate Backgrounds
- Change background colors for emphasis. Use subtle gradients (two hues within 30° of each other).
- Add subtle repeating patterns (keep low contrast with background).
- Include simple geometric shapes or illustrations at specific positions.

### Empty States
- Design empty states as a priority, not an afterthought.
- Use illustrations and clear CTAs. Hide supporting UI (filters, tables) until content exists.

### Use Fewer Borders
- Instead of borders, try: box shadows, different background colors, or extra spacing.
- `box-shadow: 0 5px 15px 0 hsla(0, 0%, 0%, 0.15)` can replace a border.

### Think Outside the Box
- Dropdowns can have sections, columns, icons, and supporting text.
- Tables can combine related columns, add images, and use color.
- Radio buttons can become selectable cards.
