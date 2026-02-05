# UI Design Skills for Claude Code

A collection of Claude Code skills that provide UI design knowledge — color palettes, typography, component patterns, layout principles, and WCAG 2.2 accessibility guidelines.

Install as a plugin and Claude Code will automatically apply the right design skill when you're working on UI code.

## Skills

| Skill | What it covers |
|-------|---------------|
| **color-palettes** | 12 color palettes with hex/HSL values in a 50–900 shade scale. Primary, neutral, and supporting colors. |
| **font-recommendations** | Curated typeface catalog with weights, licensing, CSS snippets, and font pairing tables. |
| **component-gallery** | Reference patterns with concrete CSS values for buttons, forms, cards, modals, navs, tables, and more. |
| **ui-design-principles** | Visual hierarchy, whitespace, spacing scales, layout, shadows/elevation, and responsive design. |
| **wcag-2.2** | WCAG 2.2 Level A + AA accessibility guidelines with actionable implementation rules. |

## Installation

Add this repository as a Claude Code plugin:

```bash
claude plugin marketplace add svengraziani/ui-design
```

Or clone and reference it in your project's `.claude/plugins.json`.

## Usage

The skills are loaded automatically based on context. When you ask Claude Code to work on UI code, it will apply the relevant skill. For example:

- *"Add a card component"* loads **component-gallery**
- *"Pick colors for a dashboard"* loads **color-palettes**
- *"Choose a font pairing"* loads **font-recommendations**
- *"Check this form for accessibility"* loads **wcag-2.2**
- *"Fix the spacing on this layout"* loads **ui-design-principles**

You can also invoke skills directly with slash commands (e.g. `/color-palettes`).

## Author

Sven Graziani
