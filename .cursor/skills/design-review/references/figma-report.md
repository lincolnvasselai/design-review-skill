# Figma report

## Placement

- Create one Section named `Design review / <JIRA-KEY> / <YYYY-MM-DD>` on the same page as the reviewed frames.
- Place it 400px to the right of the right-most reviewed frame, with its top aligned to the top-most reviewed frame.
- Put every review node inside that section, except the pins. Pins sit over the design frames, so put them in a `Review pins / <JIRA-KEY>` group at the top of the page layer list. Lock that group.
- Never change design layers.

## Contents, top to bottom

1. **Summary frame** (480px wide, auto layout, vertical)
   - The Jira key with a link to the card, the Figma page name, and the date
   - A score per area, plus counts by severity
   - A "Re-review" line with how many findings are Fixed and Still open, when it applies
2. **Requirement checklist frame**
   - One row per R: ID, status chip, short text, and a link to the matched frame or "no frame"
   - Not asked items at the end
3. **Finding cards** (one per finding, 360px wide, in a wrap grid)
   - The number matching its pin, the area, and the severity chip
   - What: the issue in one sentence
   - Why: the WCAG SC, the R ID, or the heuristic number
   - Fix: a concrete suggestion, such as a color value, a size, or a state to add
4. **Missing-state placeholders**
   - One frame per missing state. It is the same size as the frame or component it belongs to, with a 2px dashed border and a `Missing: <state>` label.
   - Name it `Missing / <element> / <state>`.
5. **PM questions frame** with the Unclear requirements.

## Pins

- A 24px circle with the finding number, placed on the top-left corner of the affected layer's bounding box.
- The pin color matches the severity.
- Pins at the same spot are offset by 28px.
- Do not build the pin group with `$fig.group`. That group renders a white box over its whole bounds and hides the designs. Create the pins with `$fig`, flush with `await $fig.done()`, then group the real pin nodes with `figma.group(pins, page)`, name the group, and lock it.
- After grouping, compare one pin with its target's `absoluteBoundingBox`. If they differ, move the whole group by that difference, then check two more pins.
- Take a screenshot of the whole page after writing. Any large white or empty area over the designs means something went wrong.
- Screenshots of a frame or section do not show the pins, because they are page-level nodes. Verify the pins by their positions, not by screenshots.

## Colors

Use fixed review colors so the review never picks up the brand's variables. All chips and pins use white text, and each color passes 4.5:1 against white:

| Use | Color |
|---|---|
| blocker, Missing | `#D92D20` |
| major, Partial | `#B54708` |
| minor | `#175CD3` |
| Done | `#067647` |
| Unclear | `#475467` |
| Section background | `#F9FAFB` |
| Text | `#101828` |

Use `Inter` for text. If it doesn't load, fall back to the first available font in the file.

## Re-running

1. Find an existing section whose name starts with `Design review / <JIRA-KEY>`.
2. Read its finding cards and match them to the new findings by area, element, and issue.
3. Mark the matches as Fixed or Still open in the new summary.
4. Delete the old section and its pin group, then write the new ones.
