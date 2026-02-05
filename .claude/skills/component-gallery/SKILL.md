---
name: component-gallery
description: >
  Reference patterns with CSS values for: buttons, form inputs, badges, breadcrumbs,
  pagination, horizontal/vertical/mobile navigation, tables, cards, modals, alerts,
  pricing pages, hero sections, feature grids, testimonials, footers, activity feeds,
  checkout pages, dropdowns, and empty states. Apply whenever implementing, styling, or
  reviewing a specific UI component — provides concrete sizing, padding, shadow, and
  layout values rather than abstract principles.
---

# Component Gallery

## Buttons

### Variants
- **Primary**: Bold background color (primary-500+), white text, used for main CTAs
- **Secondary**: Light background or outline, darker text, for secondary actions
- **Tertiary/Ghost**: No background, text-only with hover state, for least-important actions
- **Destructive**: Red tones, for delete/remove actions — keep smaller than primary buttons

### Sizes
- **Large**: `padding: 16px 24px; font-size: 18px;` — hero sections, marketing CTAs
- **Default**: `padding: 12px 20px; font-size: 16px;` — forms, dialogs
- **Small**: `padding: 8px 16px; font-size: 14px;` — inline actions, table rows
- **Extra Small**: `padding: 6px 12px; font-size: 12px;` — compact UIs, tags

### Design Tips
- Padding is NOT proportional to font size — larger buttons get disproportionately more generous padding
- Add subtle depth: `box-shadow: inset 0 1px 0 hsl(224, 84%, 74%); box-shadow: 0 1px 3px hsla(0,0%,0%,.2);`
- On click, reduce shadow to simulate pressing: switch from medium to small shadow
- Use brand colors for custom checkboxes/radio buttons, not browser defaults
- Consider selectable cards as alternative to radio button groups

---

## Form Inputs

### Text Inputs
- Light inset effect: `box-shadow: inset 0 2px 2px hsla(0, 0%, 0%, 0.1);`
- Adequate padding: at least `10px 12px`
- Clear focus state with ring/outline
- Labels above inputs (stacked), not beside them

### Layout
- Space between label and its input should be LESS than space between form groups
- Typical: 8px label-to-input, 24px between groups
- Use 2-column layouts for short related fields (First Name / Last Name)
- Single column for most forms — don't force 2 columns unnecessarily

### Validation
- Error messages near the field, not at the top of the form
- Red border + red text for errors
- Green checkmark for validated fields (optional)
- Don't rely on color alone — include text messages

---

## Badges / Tags

### Variants
- **Filled**: Solid background with contrasting text (e.g., white on primary-500)
- **Light**: Light tinted background with darker text (e.g., primary-50 bg + primary-700 text)
- **Outline**: Border only with matching text color
- **Dot indicator**: Small colored circle before text

### Sizes
- **Default**: `padding: 2px 8px; font-size: 12px; border-radius: 9999px;`
- **Large**: `padding: 4px 12px; font-size: 14px;`

### Usage
- Status indicators (Active, Pending, Rejected)
- Categories/labels
- Counts/notifications
- Use light variants over filled for less visual noise in tables

---

## Breadcrumbs

### Pattern
```
Home > Category > Subcategory > Current Page
```

### Design Tips
- Use a separator (>, /, chevron icon) between items
- De-emphasize all items except the current page
- Current page should not be a link
- Keep font size small (12-14px)
- Use lighter text color for separators

---

## Pagination

### Variants
- **Numbered**: `< 1 2 3 ... 10 >` — standard for search results
- **Prev/Next only**: Simpler, for sequential content
- **Load More button**: Single button, good for feeds
- **Infinite scroll**: Auto-load, for social feeds

### Design Tips
- Highlight current page with primary color background
- Disabled state for prev/next at boundaries
- Include first/last page shortcuts for large page counts
- Keep touch targets at least 44x44px on mobile

---

## Navigation

### Horizontal Navigation
- **Top bar**: Logo left, links center or right, CTA button far right
- **Tab style**: Underline or background highlight for active state
- Active indicator: colored bottom border (`border-bottom: 2px solid primary-500`)
- Keep items to 5-7 max; use dropdown for overflow

### Vertical / Sidebar Navigation
- Full-height sidebar, typically 240-280px wide (FIXED width, not percentage)
- Group related items with section headers
- Active state: background highlight + left border accent or bold text
- Icons optional but helpful for recognition
- Collapse to icons-only on smaller screens

### Mobile Navigation
- Hamburger menu for most apps
- Bottom tab bar for primary navigation (iOS pattern)
- Keep bottom nav to 3-5 items max

---

## Tables

### Design Tips
- Right-align numbers for easy comparison
- Combine related columns to reduce width (name + role in one column with hierarchy)
- Add profile images/avatars where appropriate
- Use colored badges for status columns
- Zebra striping optional — extra spacing between rows can work better
- Don't force percentage-based column widths; let content determine width
- Use `white-space: nowrap` for columns that shouldn't wrap

### Patterns
- **Simple table**: Headers + rows, minimal borders
- **Rich table**: Avatars, badges, combined columns, actions column
- **Condensed**: Tighter padding for data-dense dashboards

---

## Cards

### Anatomy
- Optional image/media at top
- Title (16-20px, bold)
- Description (14-16px, secondary color)
- Metadata (12-14px, tertiary color)
- Optional footer with actions

### Design Tips
- Use accent borders at the top for visual interest
- Subtle shadow: `box-shadow: 0 1px 3px hsla(0,0%,0%,.12), 0 1px 2px hsla(0,0%,0%,.24);`
- Consistent image aspect ratios with `object-fit: cover`
- Cards crossing background transitions create depth (overlap technique)

---

## Modals / Dialogs

### Design Tips
- Large shadow for prominence: `box-shadow: 0 15px 35px hsla(0,0%,0%,.2);`
- Semi-transparent backdrop: `background-color: rgba(0, 0, 0, .5);`
- Max-width constraint (400-600px for forms, up to 800px for complex content)
- Clear close action (X button top-right, Cancel button bottom)
- Focus trap for accessibility
- Destructive confirmations: make the destructive button less prominent (not big and red)

---

## Alerts / Notifications

### Variants
- **Info**: Blue tinted (blue-50 bg, blue-700 text, blue-500 left border)
- **Success**: Green tinted
- **Warning**: Yellow tinted
- **Error**: Red tinted

### Design Tips
- Colored left border accent (4px) is a classic, effective pattern
- Use icon + text, don't rely on color alone
- Light background with darker text of the same hue
- Dismissible with X button for non-critical alerts

### CSS Pattern
```css
.alert-info {
  background-color: /* primary-50 */;
  color: /* primary-900 */;
  border-left: 4px solid /* primary-500 */;
}
```

---

## Pricing Pages

### Layout
- 2-4 plan options side by side
- Highlight recommended plan (accent border, raised with shadow, or "Popular" badge)
- Feature comparison list with checkmarks
- CTA button for each plan

### Design Tips
- Price should be the most prominent element
- Use hierarchy: Plan name (small, uppercase, letter-spaced) > Price (large, bold) > Period (small, muted)
- De-emphasize less popular plans
- Toggle between monthly/annual billing

---

## Marketing Sections

### Hero Section
- Large headline (36-72px)
- Supporting paragraph (18-20px, max 45-75 chars per line)
- Primary CTA button + optional secondary CTA
- Optional image/illustration to the right or below

### Feature Sections
- 3-4 features in a grid
- Icon + heading + short description per feature
- Icons in colored shapes (don't scale up small icons — wrap them in a background shape)
- Center-aligned text works for short descriptions (2-3 lines max)

### Testimonials
- Large quotation marks as visual element (oversized, colored)
- Quote text in larger font or italic
- Attribution: name, title, company, optional photo

---

## Footers

### Content
- Logo + short description
- Navigation links in columns (Product, Company, Resources, Legal)
- Social media links
- Newsletter signup
- Copyright notice

### Design Tips
- Different background color from main content (darker)
- 3-4 columns on desktop, stacked on mobile
- Keep link font size small (14px)
- Subtle separators between sections

---

## Activity Feeds

### Pattern
- Avatar + name + action + timestamp per entry
- Vertical timeline line connecting entries
- Group by date
- Different icons/colors for different action types

---

## Checkout / E-Commerce

### Cart
- Product image + name + price + quantity controls + remove button
- Fixed containers for product images (`object-fit: cover`)
- Subtotal, taxes, total summary
- Prominent checkout CTA

### Design Tips
- Don't make everything full-width — constrain to comfortable reading width
- Use hierarchy: total price > individual prices > metadata
- Progress indicator for multi-step checkout

---

## Dropdowns

### Beyond Basic Lists
- Break into sections with headers
- Use multiple columns for many options
- Add supporting text or descriptions per item
- Include icons for visual recognition
- "NEW" badges for recently added options
- Search/filter for long lists

---

## Empty States

### Design Tips
- Treat as a first impression — don't just show "No items found"
- Include illustration or icon
- Clear call-to-action explaining what to do next
- Hide filters/table headers/controls until content exists
- Make it encouraging and helpful

---

## General Component Principles

### Separation Without Borders
1. **Box shadow**: `box-shadow: 0 5px 15px 0 hsla(0, 0%, 0%, 0.15);`
2. **Different background colors**: Adjacent elements with slightly different backgrounds
3. **Extra spacing**: Increase space between elements instead of adding lines

### Accent Borders for Polish
- Top of cards: `border-top: 4px solid primary-500;`
- Active nav items: `border-bottom: 2px solid primary-500;`
- Side of alerts: `border-left: 4px solid primary-500;`
- Under headlines: Short colored underline
- Top of layout: Full-width thin colored bar

### Depth Techniques
- Raised: lighter top edge + small drop shadow
- Inset: darker top edge + lighter bottom edge
- Overlapping: elements crossing background transitions
- Color: lighter = closer, darker = further

### Responsive Patterns
- Start mobile-first (~400px)
- Sidebars: fixed width, not percentage-based
- Don't shrink elements until necessary (use max-width)
- Large elements shrink faster than small ones
- Button padding: not proportional — adjust independently from font size
