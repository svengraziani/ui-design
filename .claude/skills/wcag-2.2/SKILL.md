---
name: wcag-2.2
description: >
  WCAG 2.2 accessibility guidelines with actionable implementation rules for web developers.
  Covers contrast ratios, keyboard navigation, focus management, ARIA, screen readers, alt text,
  touch targets, form validation, color blindness, reduced motion, semantic HTML, and landmarks.
  Apply whenever writing HTML/CSS/JS, building forms, handling focus, choosing colors for
  accessibility, implementing interactive components, or reviewing code for a11y compliance.
  Includes all Level A + AA criteria and new 2.2 additions (focus not obscured, dragging
  alternatives, target size minimum, redundant entry, accessible authentication, consistent help).
---

# WCAG 2.2 — Accessibility Guidelines for Developers

## Quick Reference: Contrast Ratios

| Element | Minimum ratio | Rule |
|---------|--------------|------|
| Normal text (<18px / <14px bold) | **4.5:1** | 1.4.3 AA |
| Large text (>=18px / >=14px bold) | **3:1** | 1.4.3 AA |
| UI components & graphical objects | **3:1** | 1.4.11 AA |
| Enhanced (AAA) normal text | **7:1** | 1.4.6 AAA |
| Enhanced (AAA) large text | **4.5:1** | 1.4.6 AAA |
| Focus indicator vs adjacent | **3:1** | 2.4.13 AAA |

## Quick Reference: Target Sizes

| Level | Minimum | Rule |
|-------|---------|------|
| AA | **24x24 CSS px** (or adequate spacing) | 2.5.8 NEW |
| AAA | **44x44 CSS px** | 2.5.5 |

---

## 1. Perceivable

### Images & Non-text Content (1.1.1 A)
- Every `<img>` needs `alt` text. Decorative images: `alt=""`
- Informative images: describe the content, not the appearance
- Complex images (charts, diagrams): provide long description nearby or via `aria-describedby`
- Icon buttons: `aria-label` on the button, `aria-hidden="true"` on the icon
- `<svg>`: use `role="img"` + `aria-label` or `<title>` inside

```html
<!-- Informative -->
<img src="chart.png" alt="Sales increased 40% in Q3 2024">

<!-- Decorative -->
<img src="divider.svg" alt="" role="presentation">

<!-- Icon button -->
<button aria-label="Close dialog">
  <svg aria-hidden="true">...</svg>
</button>
```

### Video & Audio (1.2.x A/AA)
- Prerecorded video: provide captions (1.2.2 A) and audio descriptions (1.2.3 A)
- Audio-only: provide text transcript (1.2.1 A)
- Live video: provide live captions (1.2.4 AA)

### Semantic Structure (1.3.1 A)
- Use semantic HTML: `<nav>`, `<main>`, `<aside>`, `<header>`, `<footer>`, `<section>`
- Heading hierarchy: one `<h1>`, don't skip levels (h1 -> h3)
- Lists: `<ul>/<ol>/<dl>`, not `<div>` with bullets
- Tables: `<th scope="col/row">`, `<caption>`, never for layout
- Forms: `<label for="id">`, `<fieldset>/<legend>` for groups

```html
<form>
  <fieldset>
    <legend>Shipping Address</legend>
    <label for="street">Street</label>
    <input id="street" type="text" autocomplete="street-address">
  </fieldset>
</form>
```

### Reading Order (1.3.2 A)
- DOM order must match visual order
- Don't use CSS (`order`, `flex-direction: row-reverse`) to reorder visually if it breaks reading sequence
- Test: disable CSS and check if content still makes sense

### Sensory Characteristics (1.3.3 A)
- Never rely solely on color, shape, size, or position to convey meaning
- "Click the red button" -> "Click the Delete button (red)"
- "See the chart on the right" -> "See the Sales Chart (Figure 3)"

### Orientation (1.3.4 AA)
- Don't lock content to portrait or landscape
- `@media (orientation: portrait)` is fine for styling, but don't hide content

### Input Purpose (1.3.5 AA)
- Use `autocomplete` attributes on form fields that collect personal data

```html
<input type="text" autocomplete="given-name">
<input type="email" autocomplete="email">
<input type="tel" autocomplete="tel">
<input type="text" autocomplete="street-address">
<input type="text" autocomplete="postal-code">
<input type="text" autocomplete="cc-number">
```

### Color Alone (1.4.1 A)
- Never use color as the only way to convey information
- Error states: red border + icon + text message
- Links in paragraphs: underline or 3:1 contrast to surrounding text + underline on hover/focus
- Charts: use patterns/shapes in addition to colors
- Status indicators: color + icon + text label

```css
/* Bad: only color */
.error { color: red; }

/* Good: color + icon + text */
.error {
  color: #CF1124;
  border-left: 4px solid #CF1124;
}
.error::before { content: "⚠ "; }
```

### Contrast (1.4.3 AA, 1.4.11 AA)
- **Text**: 4.5:1 minimum (3:1 for large text >=18px or >=14px bold)
- **UI components**: 3:1 for borders, icons, focus indicators, form controls against adjacent colors
- **Disabled elements**: exempt from contrast requirements
- **Placeholder text**: must meet 4.5:1 if it conveys information

```css
/* Meets 4.5:1 on white */
color: #595959; /* 7:1 — safe */
color: #767676; /* 4.54:1 — minimum for normal text */

/* Meets 3:1 on white for UI components */
border-color: #949494; /* 3.03:1 */
```

### Resize (1.4.4 AA)
- Text must be resizable to 200% without loss of content
- Use `rem`/`em` for font sizes, not `px`
- Don't use `max-height` with `overflow: hidden` on text containers
- Test: browser zoom to 200%

### Reflow (1.4.10 AA)
- No horizontal scrolling at 320px viewport width (vertical content)
- No vertical scrolling at 256px viewport height (horizontal content)
- Exceptions: data tables, maps, diagrams, toolbars
- Test: set viewport to 1280px and zoom to 400%

```css
/* Good: responsive container */
.container { max-width: 100%; overflow-wrap: break-word; }

/* Bad: fixed width forcing scroll */
.container { width: 1200px; }
```

### Text Spacing (1.4.12 AA)
- No content loss when users override:
  - Line height: 1.5x font size
  - Paragraph spacing: 2x font size
  - Letter spacing: 0.12x font size
  - Word spacing: 0.16x font size
- Don't set fixed heights on containers with text
- Test with browser extension or custom CSS:

```css
* {
  line-height: 1.5em !important;
  letter-spacing: 0.12em !important;
  word-spacing: 0.16em !important;
}
p { margin-bottom: 2em !important; }
```

### Hover/Focus Content (1.4.13 AA)
- Tooltips, popovers triggered by hover/focus must be:
  1. **Dismissible**: Esc key closes without moving focus
  2. **Hoverable**: user can move pointer over the new content without it disappearing
  3. **Persistent**: stays visible until user dismisses, moves focus, or info becomes invalid

```css
/* Good: hoverable tooltip */
.tooltip-trigger:hover + .tooltip,
.tooltip-trigger:focus + .tooltip,
.tooltip:hover {
  display: block;
}
```

---

## 2. Operable

### Keyboard Access (2.1.1 A, 2.1.2 A)
- All interactive elements must be keyboard-operable
- Use native elements: `<button>`, `<a href>`, `<input>`, `<select>`
- Custom widgets: add `tabindex="0"` + keyboard event handlers
- No keyboard traps: user must always be able to Tab away
- `tabindex="-1"`: focusable via JS only (e.g., modal containers)
- `tabindex="0"`: in natural tab order
- Never use `tabindex` > 0

```html
<!-- Bad: div with click handler only -->
<div onclick="doThing()">Click me</div>

<!-- Good: button -->
<button onclick="doThing()">Click me</button>

<!-- Good: custom widget with keyboard support -->
<div role="button" tabindex="0"
     onclick="doThing()"
     onkeydown="if(event.key==='Enter'||event.key===' ')doThing()">
  Click me
</div>
```

### Character Key Shortcuts (2.1.4 A)
- If using single-character shortcuts (e.g., "s" to search): allow users to remap or disable them
- Better: require modifier key (Ctrl+S, not just S)

### Timing (2.2.1 A, 2.2.2 A)
- Session timeouts: warn 20+ seconds before, allow 10+ extensions
- Auto-moving content (carousels, tickers): provide pause/stop button
- Auto-refreshing: allow users to control update frequency

### Flashing Content (2.3.1 A)
- Nothing flashes more than 3 times per second
- Avoid flashing entirely when possible

### Skip Navigation (2.4.1 A)
- Provide "Skip to main content" link as first focusable element

```html
<body>
  <a href="#main" class="skip-link">Skip to main content</a>
  <nav>...</nav>
  <main id="main">...</main>
</body>
```

```css
.skip-link {
  position: absolute;
  top: -40px;
  left: 0;
  padding: 8px 16px;
  z-index: 100;
}
.skip-link:focus {
  top: 0;
}
```

### Page Titles (2.4.2 A)
- Every page needs a unique, descriptive `<title>`
- Pattern: "Page Name — Site Name" or "Page Name | Site Name"

### Focus Order (2.4.3 A)
- Tab order must follow logical reading order
- Modals: trap focus inside until dismissed
- Dynamic content: manage focus when content appears/disappears

### Link Purpose (2.4.4 A)
- Link text must make sense in context
- Avoid "click here", "read more", "learn more" without context
- Use `aria-label` or `aria-describedby` when visual context is needed

```html
<!-- Bad -->
<a href="/plans">Read more</a>

<!-- Good -->
<a href="/plans">View pricing plans</a>

<!-- Good: when visual design needs "Read more" -->
<a href="/plans" aria-label="Read more about pricing plans">Read more</a>
```

### Headings and Labels (2.4.6 AA)
- Headings must describe the section content
- Form labels must describe what's expected
- Don't use placeholder as sole label

### Focus Visible (2.4.7 AA)
- Keyboard focus must always be visible
- Never: `outline: none` without a replacement
- Custom focus styles must be clearly visible

```css
/* Good: custom focus style */
:focus-visible {
  outline: 2px solid #0967D2;
  outline-offset: 2px;
}

/* Remove default only when providing custom */
:focus:not(:focus-visible) {
  outline: none;
}
```

### Focus Not Obscured (2.4.11 AA) — NEW in 2.2
- Focused element must not be entirely hidden by sticky headers, footers, cookie banners, etc.
- Use `scroll-padding` to account for fixed elements

```css
html {
  scroll-padding-top: 80px;  /* height of sticky header */
  scroll-padding-bottom: 60px; /* height of sticky footer */
}
```

### Focus Appearance (2.4.13 AAA) — NEW in 2.2
- Focus indicator: minimum 2px thick outline or equivalent area
- 3:1 contrast ratio between focused and unfocused state
- Must not be obscured by other content

### Pointer Gestures (2.5.1 AA)
- Multi-point gestures (pinch, multi-finger swipe) need single-pointer alternative
- Path-based gestures (drag-to-draw) need alternative unless essential

### Pointer Cancellation (2.5.2 AA)
- Don't trigger actions on mouse-down — use click (up-event)
- Allow aborting by moving pointer away before releasing

### Label in Name (2.5.3 AA)
- The accessible name must contain the visible label text
- If a button says "Search", the `aria-label` can be "Search products" but not "Find items"

### Dragging Movements (2.5.7 AA) — NEW in 2.2
- Any drag-and-drop interaction must have a non-dragging alternative
- Example: drag to reorder -> also provide up/down buttons

```html
<!-- Drag-to-reorder with button alternatives -->
<li draggable="true">
  <span>Item 1</span>
  <button aria-label="Move Item 1 up">↑</button>
  <button aria-label="Move Item 1 down">↓</button>
</li>
```

### Target Size Minimum (2.5.8 AA) — NEW in 2.2
- Interactive targets: minimum **24x24 CSS pixels**
- Or: sufficient spacing so the 24px circle around center doesn't overlap other targets
- Exceptions: inline links in text, browser-default controls, essential size

```css
/* Meets 2.5.8 */
button, a, input, select, [role="button"] {
  min-width: 24px;
  min-height: 24px;
}

/* Better: aim for 44x44 (2.5.5 AAA) */
.touch-target {
  min-width: 44px;
  min-height: 44px;
  padding: 12px;
}
```

---

## 3. Understandable

### Language (3.1.1 A, 3.1.2 AA)
- Set `lang` attribute on `<html>`: `<html lang="en">`
- Mark language changes inline: `<span lang="de">Danke</span>`

### Predictable Behavior (3.2.1 A, 3.2.2 A)
- Focus alone must not trigger unexpected actions (no auto-submit on focus)
- Input changes should not trigger unexpected navigation
- If they do: warn user beforehand

### Consistent Navigation (3.2.3 AA, 3.2.4 AA)
- Navigation order and labeling must be consistent across pages
- Same function = same name everywhere (don't call it "Search" on one page and "Find" on another)

### Consistent Help (3.2.6 A) — NEW in 2.2
- Help mechanisms (contact info, chat, FAQ links) must appear in the same relative position across pages
- If footer has "Contact Us" link, it should be in the footer on every page

### Error Identification (3.3.1 A)
- Automatically detected errors: identify the field and describe the error in text
- Don't rely on color alone for error indication

```html
<label for="email">Email</label>
<input id="email" type="email" aria-describedby="email-error" aria-invalid="true">
<p id="email-error" role="alert" class="error">
  Please enter a valid email address (e.g., name@example.com)
</p>
```

### Labels and Instructions (3.3.2 A)
- Visible label for every form field
- Required fields: indicate in label, not just with `*`
- Complex formats: provide instruction text

```html
<label for="phone">
  Phone number <span class="required">(required)</span>
</label>
<input id="phone" type="tel" aria-describedby="phone-hint" required>
<p id="phone-hint" class="hint">Format: +1 (555) 123-4567</p>
```

### Error Suggestions (3.3.3 AA)
- When an error is detected and suggestions are known: provide them
- "Invalid date" -> "Please enter date as DD/MM/YYYY"

### Error Prevention (3.3.4 AA)
- Legal, financial, or data-altering submissions must be:
  - **Reversible**: allow undo, OR
  - **Checked**: validate before final submit, OR
  - **Confirmed**: review + confirm step

### Redundant Entry (3.3.7 A) — NEW in 2.2
- Don't make users re-enter data already submitted in the same session
- Auto-populate or allow selection from previously entered values
- Exception: re-entering password for security

### Accessible Authentication (3.3.8 AA) — NEW in 2.2
- Don't require cognitive function tests (puzzles, memorization) as sole auth method
- Allow: password managers, passkeys, biometrics, email/SMS codes
- CAPTCHAs: provide alternative method (audio, email verification)
- Copy-paste must not be blocked in password fields

---

## 4. Robust

### Name, Role, Value (4.1.2 A)
- Custom components must expose correct ARIA role, name, state
- Use native elements when possible — they provide this for free

```html
<!-- Custom toggle: needs role + state -->
<button role="switch" aria-checked="false" onclick="toggle(this)">
  Dark mode
</button>

<!-- Custom tab panel -->
<div role="tablist">
  <button role="tab" aria-selected="true" aria-controls="panel-1">Tab 1</button>
  <button role="tab" aria-selected="false" aria-controls="panel-2">Tab 2</button>
</div>
<div role="tabpanel" id="panel-1">Content 1</div>
<div role="tabpanel" id="panel-2" hidden>Content 2</div>
```

### Status Messages (4.1.3 AA)
- Status messages (success, error, progress) must be announced by screen readers without receiving focus
- Use `role="status"` (polite) or `role="alert"` (assertive)
- Use `aria-live="polite"` for non-urgent updates

```html
<!-- Toast notification -->
<div role="status" aria-live="polite">
  Your changes have been saved.
</div>

<!-- Error alert -->
<div role="alert">
  Payment failed. Please check your card details.
</div>

<!-- Live region for dynamic content -->
<div aria-live="polite" aria-atomic="true">
  Showing 1-10 of 42 results
</div>
```

---

## ARIA Cheat Sheet

### Landmarks
```html
<header role="banner">         <!-- site header, once per page -->
<nav role="navigation">         <!-- navigation, label with aria-label if multiple -->
<main role="main">              <!-- main content, once per page -->
<aside role="complementary">    <!-- sidebar, related content -->
<footer role="contentinfo">     <!-- site footer, once per page -->
<form role="search">            <!-- search form -->
```

### Common Patterns
```html
<!-- Modal dialog -->
<div role="dialog" aria-modal="true" aria-labelledby="dialog-title">
  <h2 id="dialog-title">Confirm deletion</h2>
  <p>Are you sure?</p>
  <button>Cancel</button>
  <button>Delete</button>
</div>

<!-- Accordion -->
<h3>
  <button aria-expanded="false" aria-controls="section-1">Section Title</button>
</h3>
<div id="section-1" role="region" hidden>Content</div>

<!-- Loading state -->
<div aria-busy="true" aria-live="polite">Loading...</div>

<!-- Progress -->
<div role="progressbar" aria-valuenow="75" aria-valuemin="0" aria-valuemax="100">
  75%
</div>
```

### States to manage
| State | Use for |
|-------|---------|
| `aria-expanded` | Accordions, dropdowns, menus |
| `aria-selected` | Tabs, listbox options |
| `aria-checked` | Checkboxes, switches, toggles |
| `aria-pressed` | Toggle buttons |
| `aria-current="page"` | Active nav item |
| `aria-invalid="true"` | Form fields with errors |
| `aria-disabled="true"` | Non-interactive disabled state |
| `aria-hidden="true"` | Decorative elements, hidden from AT |
| `aria-busy="true"` | Region currently updating |

---

## Reduced Motion

```css
@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
    scroll-behavior: auto !important;
  }
}
```

## Color Scheme Preference

```css
@media (prefers-color-scheme: dark) {
  :root {
    --bg: #1F2933;
    --text: #F5F7FA;
  }
}
```

---

## Testing Checklist

### Keyboard
- [ ] Tab through entire page — logical order, no traps
- [ ] All interactive elements reachable and operable
- [ ] Focus indicator always visible
- [ ] Esc closes modals/popovers
- [ ] Enter/Space activates buttons and links

### Screen Reader
- [ ] All images have appropriate alt text
- [ ] Headings form logical outline (h1 > h2 > h3)
- [ ] Form fields have associated labels
- [ ] Error messages announced (`role="alert"`)
- [ ] Dynamic content changes announced (`aria-live`)
- [ ] Page title is descriptive

### Visual
- [ ] Text contrast >=4.5:1 (3:1 for large text)
- [ ] UI component contrast >=3:1
- [ ] Content readable at 200% zoom
- [ ] No horizontal scroll at 320px width
- [ ] Information not conveyed by color alone
- [ ] Touch targets >=24x24px (AA) or >=44x44px (AAA)

### Motion
- [ ] No content flashes >3 times/second
- [ ] Animations respect `prefers-reduced-motion`
- [ ] Auto-playing content has pause/stop controls

### Forms
- [ ] Every field has visible label
- [ ] Required fields clearly marked
- [ ] Error messages describe issue and suggest fix
- [ ] Autocomplete attributes on personal data fields
- [ ] No re-entry of previously submitted data (2.2 NEW)
- [ ] Authentication doesn't require cognitive tests (2.2 NEW)
