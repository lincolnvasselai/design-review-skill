# Accessibility

Target is WCAG 2.2 AA. These checks can be done in Figma. Cite the success criterion on each finding.

## Contrast

Read the text fill and the nearest solid fill behind it. Resolve variables to their values in the active mode. Compute the contrast ratio from relative luminance.

| Element | Minimum | SC |
|---|---|---|
| Body text (under 24px, or under 18.66px bold) | 4.5:1 | 1.4.3 |
| Large text (24px+, or 18.66px+ bold) | 3:1 | 1.4.3 |
| Icons, input borders, focus rings, chart lines | 3:1 against the adjacent color | 1.4.11 |
| Disabled controls | exempt, but flag them as minor if they're unreadable | 1.4.3 |

Text over an image or gradient is an estimate from the screenshot. Say so, and suggest an overlay or a scrim.

When the file has light and dark modes, check both.

## Size and spacing

- Target size of at least 24x24px, or spacing that keeps a 24px circle clear (SC 2.5.8). Recommend 44x44px on touch screens.
- Body text of at least 14px on desktop and 16px on mobile. This is a recommendation, so flag smaller text as minor.
- Line height of at least 1.4 for body text.

## Meaning and labels

- Color alone (SC 1.4.1): error, success, required, selected, and chart series need a second cue, such as an icon, text, or a pattern.
- Every input has a visible label. A placeholder is not a label (SC 3.3.2).
- Icon-only buttons have an accessible name noted in an annotation or the layer name (SC 4.1.2).
- Error messages sit next to the field and say how to fix it (SC 3.3.1, 3.3.3).
- Links are distinguishable from text by something other than color.

## Focus and order

- Every interactive component has a focus state with a visible ring of at least 2px and 3:1 contrast (SC 2.4.7, 2.4.11).
- Focus is not hidden by sticky headers, cookie bars, or modals (SC 2.4.11).
- The reading and focus order follows the layout. Flag layouts where the visual order and the layer order clearly differ.
- Modals and drawers have a close control and a stated focus return.

## Structure and content

- One clear heading per screen and a heading hierarchy that doesn't skip levels. Check the text style names.
- Images that carry meaning have alt text noted. Decorative images are marked decorative.
- Motion and auto-play have a pause option (SC 2.2.2).
- Reflow: a 320px wide frame exists, or the layout uses auto layout that can reflow (SC 1.4.10).
- Dragging has a single-pointer alternative (SC 2.5.7).
- Repeated help and contact appear in the same place across screens (SC 3.2.6).
- Login doesn't rely on memory puzzles alone (SC 3.3.8).

## Out of scope in Figma

List these as "verify in code" instead of failing them: screen reader output, keyboard traps, zoom at 200%, live regions, and real focus behavior.
