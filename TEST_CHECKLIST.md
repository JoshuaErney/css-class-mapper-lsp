# Test Checklist

Manual test cases for each release. Check off every item before tagging.

---

## Setup

- Two files open side by side: `index.html` and `styles.css`
- A few classes already defined in CSS (e.g. `.btn`, `.btn-primary`, `.card`)

---

## 1. File Watcher (v0.7.1 fix — highest priority)

These tests verify the core bug that was fixed: the class map staying current as CSS files change.

- [ ] Add a new class (`.new-class {}`) to `styles.css` and save — the "Unknown CSS class" squiggle in the HTML file clears without restarting the editor
- [ ] Delete a class from `styles.css` and save — a new "Unknown CSS class" squiggle appears in the HTML wherever it was used
- [ ] Create a brand-new CSS file in the workspace and save it with a class — that class becomes available in completions and diagnostics clear
- [ ] Delete a CSS file from the workspace — all classes that came only from that file are flagged as unknown in HTML

---

## 2. Diagnostics

- [ ] A class used in HTML that has no CSS definition shows an error squiggle
- [ ] Squiggle covers exactly the class token (not surrounding whitespace or quotes)
- [ ] A valid class shows no squiggle
- [ ] Multiple unknown classes on the same element each get their own squiggle
- [ ] A class inside a multi-line `class="foo\n  bar"` attribute is flagged correctly on the right line
- [ ] Defining the same class twice in one CSS file produces a warning on the second definition
- [ ] The duplicate warning disappears if you remove the second definition and save

---

## 3. Autocomplete

- [ ] Typing inside `class=""` opens a completion list showing all defined CSS classes
- [ ] Typing a prefix (e.g. `bt`) filters to matching classes
- [ ] Typing in uppercase (e.g. `BTN`) still matches `btn` (case-insensitive)
- [ ] A class already in the attribute is excluded from suggestions
- [ ] Inserting a completion next to an existing class adds a space automatically (no double-spaces, no missing spaces)
- [ ] A newly added CSS class appears in completions after saving the CSS file (file watcher)

---

## 4. Hover

- [ ] Hovering over a known class shows the selector, `source-file:line`, specificity `(a,b,c)`, and CSS properties
- [ ] Hovering over a class inside an `@media` block shows the media query context (_inside `@media (max-width: 768px)`_)
- [ ] A class defined in multiple CSS files shows all definitions numbered
- [ ] Hex / `rgb()` / `hsl()` values in properties appear in the color summary line
- [ ] Hovering over a `--custom-property` inside `style=""` shows its value
- [ ] Hovering over an unknown class shows nothing (no tooltip)

---

## 5. Go to Definition

- [ ] Cmd+Click on a class name in `class=""` jumps to its definition in the CSS file
- [ ] A class defined in multiple files shows a picker with all locations
- [ ] Cmd+Click on an ID in `id=""` jumps to the `#id` rule in the CSS file

---

## 6. Find References

- [ ] Find References on a class in a CSS file lists every HTML attribute usage across the workspace
- [ ] Find References on an ID works the same way
- [ ] A class used zero times returns an empty list

---

## 7. Rename

- [ ] Renaming a class updates the CSS selector and every HTML attribute in the workspace
- [ ] Renaming `.btn` does **not** change `.btn-primary` (word-boundary check)
- [ ] Renaming to a digit-starting name (e.g. `2col`) is rejected with an error
- [ ] Renaming an ID works the same way

---

## 8. Code Action — Create Class/ID

- [ ] An unknown class squiggle offers a Quick Fix: "Create CSS class .name in styles.css"
- [ ] Applying the Quick Fix appends `.name { }` to the CSS file
- [ ] After the fix is applied the squiggle clears
- [ ] An unknown ID squiggle offers a Quick Fix for `#name` instead
- [ ] The Quick Fix targets a CSS file in the same directory as the HTML file when one exists

---

## 9. CSS Variables

- [ ] Typing `--` inside `style=""` opens completions showing all custom properties
- [ ] Typing a prefix (e.g. `--color`) filters the list
- [ ] Hovering over a `--variable` in `style=""` shows its value

---

## 10. @import

- [ ] Classes defined only in an `@import`-ed CSS file appear in completions and diagnostics
- [ ] A circular `@import` chain does not hang or crash the LSP

---

## 11. Unused Selector Hint

- [ ] A CSS class that isn't used in any open HTML file is flagged with a hint on its definition line
- [ ] When the class is added to an open HTML file the hint disappears
- [ ] No hints appear when no HTML files are open

---

## 12. ID Attribute

- [ ] Completions work inside `id=""`
- [ ] Once the `id` attribute has a value, no further completions are offered (single-value guard)
- [ ] Hover, go-to-definition, and find references all work inside `id=""`

---

## 13. Edge Cases

- [ ] A CSS file over 500 KB is skipped (no crash, no stall)
- [ ] A document with non-ASCII characters (accented letters, em-dashes) doesn't crash or produce wrong positions
- [ ] `node_modules/` and hidden directories (`.cache/`) are excluded from scanning
