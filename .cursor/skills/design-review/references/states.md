# States

## Matrix

| Kind | Required states | Often forgotten |
|---|---|---|
| Button, link, icon button | default, hover, focus, pressed, disabled | loading, destructive, selected |
| Text input, textarea, select | empty, focus, filled, error, disabled | read-only, success, helper text, character limit, autofill |
| Checkbox, radio, switch | off, on, focus, disabled | indeterminate, error |
| Tabs, chips, segmented control | default, selected, hover, focus | disabled, overflow with many items |
| Menu, dropdown, combobox | closed, open, option hover, option selected | no results, loading options, long option text |
| Modal, drawer, toast | open, close control | stacked toasts, long content scroll, mobile size |
| List, table, grid | populated | loading or skeleton, empty, error, one item, many items, pagination or infinite scroll, sort and filter active |
| Screen or page | default | loading, empty first use, empty after filter, error, offline, no permission, partial data, success |
| Form flow | each step | validation errors, submitting, submit error, success, back or cancel |
| Media | loaded | loading, broken image, missing image fallback |

Add any breakpoints the card or spec names: mobile, tablet, desktop.

Only check the kinds that appear in scope. A screen with no form does not need form states.

## Detecting states

Check in this order:

1. Component variant properties, such as `State=Hover` or `state: disabled`. Read the component set, not just the instance on the canvas.
2. Frame names, such as `Checkout / Empty` or `Error`.
3. Visible content in screenshots, such as a skeleton, an empty illustration, or red helper text.
4. Annotations or sticky notes that say a state is shared with another frame.

A state counts as designed when any of these shows it. When a state is used by an instance but the component set lacks it, report the component, not the screen.

When unsure, ask the user with AskQuestion instead of marking the state Missing.

## Output

For each element or screen, list the states found and the states missing. Each missing state becomes a dashed placeholder in the report. See [figma-report.md](figma-report.md).
