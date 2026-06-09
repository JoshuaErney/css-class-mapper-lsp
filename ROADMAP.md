# Roadmap

Planned features and improvements for the CSS Class Mapper extension.
Checked items have been shipped — see [CHANGELOG.md](CHANGELOG.md) for details.

---

## CSS Parsing

- [x] Handle `@import` — follow imported CSS files automatically *(v0.2.0)*
- [x] Support `@media` — capture which breakpoint a class lives in *(v0.4.0)*
- [x] Handle multiple definitions of the same class across files *(v0.3.0)*
- [x] Extract ID selectors (`#id`) alongside class selectors *(v0.4.0)*

---

## HTML Context

- [x] Complete when `class` attribute already has values (`class="btn |"`) *(v0.2.0)*
- [x] Filter out classes already used in the same `class` attribute *(v0.2.0)*
- [x] Trigger completions and hover inside `id="..."` attributes — `id` is single-value only, stop suggesting once a value exists *(v0.4.0)*
- [ ] Scope suggestions to CSS reachable from the current HTML file — `<link>` tags, inline `<style>` blocks, and `@import` chains *(deferred — requires per-document state)*

---

## Completions

- [x] Sort suggestions alphabetically *(v0.2.0)*
- [x] Recognize and complete CSS custom properties (`--primary-color`) inside `style="..."` attributes *(v0.6.0)*
- [ ] Sort by frequency of use — user-configurable *(deferred — requires usage-tracking infrastructure)*

---

## Hover Tooltips

- [x] Show the full original selector (`.btn.btn--primary`) not just the class name *(v0.3.0)*
- [x] Show which file the rule comes from *(v0.1.0)*
- [x] Show which line number the rule comes from *(v0.3.0)*
- [x] Show the media query context if the rule is inside one (`@media (max-width: 768px)`) *(v0.4.0)*
- [x] Show all definitions when multiple files define the same class or ID *(v0.3.0)*
- [x] Color swatches next to color values *(v0.6.0 — hex/rgb/hsl values shown inline)*
- [x] Show computed specificity score — IDs score `(1,0,0)`, classes `(0,1,0)` *(v0.5.0)*
- [x] Show the declared value of a CSS variable in hover tooltips *(v0.6.0)*
- [ ] Expand shorthand properties (`margin: 8px 16px` → all four sides) *(deferred — complex CSS expansion rules)*

---

## Diagnostics

- [x] Highlight class names in HTML that don't exist in any CSS file *(v0.5.0)*
- [x] Show a soft hint (faint underline, not an error) for classes and IDs that appear unused in open HTML files *(v0.6.0)*
- [x] Warn when the same class or ID is defined twice in the same CSS file *(v0.5.0)*

---

## Navigation

- [x] Go to definition — `Cmd+Click` a class in HTML to jump to its definition in the CSS file *(v0.2.0)*
- [x] Find all references — from an HTML attribute, find every HTML file that uses the same class or ID *(v0.6.0)*

---

## Refactoring

- [x] Rename — rename a class or ID in one place and update it across all CSS and HTML files *(v0.6.0)*
- [ ] Extract class — select CSS properties and turn them into a new named class *(deferred — requires editor-specific selection APIs)*

---

## Code Actions

- [x] "Create class" or "Create ID" — when an undefined class or ID is used in HTML, offer to generate it in the nearest CSS file *(v0.6.0)*
- [ ] "Remove unused class or ID" — remove a CSS rule that has no HTML references *(deferred — destructive operation, needs confidence mechanism)*

---

## Performance

- [ ] Lazy-load — only scan CSS files when an HTML file is first opened *(deferred — startup scan is fast enough for most projects)*
- [x] Cap file size — skip CSS files over 500 KB to handle minified files *(v0.6.0)*

---

## Distribution

- [x] GitHub Actions workflow to auto-compile and publish release assets on new tags *(v0.4.0)*
