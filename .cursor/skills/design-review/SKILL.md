---
name: design-review
description: >-
  Reviews a Figma design against its Jira card and linked Confluence specs.
  Checks that every requirement was designed, runs a WCAG 2.2 AA
  accessibility pass, finds missing states (hover, focus, disabled,
  loading, empty, error, and others), and adds design system, content, and
  handoff checks. Writes the review as frames, pins, and finding cards
  next to the designs in Figma. Use when the user asks to review a design,
  check a task, check accessibility, check states, run a design QA, or
  says revisar design, revisão de design, acessibilidade, or estados.
---

# Design review

Reads what was asked in Jira and Confluence, reads what was designed in Figma, and writes the gaps into the Figma file. The skill never edits design layers. It only adds a review section.

Read [references/requirements.md](references/requirements.md), [references/accessibility.md](references/accessibility.md), [references/states.md](references/states.md), [references/heuristics.md](references/heuristics.md), and [references/figma-report.md](references/figma-report.md) before starting.

Load the `figma-use` skill before any `use_figma` call. Ask in the user's language. Use AskQuestion for every choice.

## 1. Inputs

1. Ask for the Jira key and the Figma URL. Use the AskQuestion "Other" field for free text. Skip anything the user already gave.
2. Ask which checks to run. All are on by default: requirements, accessibility, states, heuristics, design system, content, handoff, edge-case data.
3. Ask the scope: the whole page, or only the frames the user names or selects.

Parse the Figma URL: `figma.com/design/:fileKey/:name?node-id=1-2` gives `fileKey` and node `1:2`. For branch URLs, use the branch key.

## 2. Requirements

Follow [references/requirements.md](references/requirements.md).

1. `getJiraIssue` gets the description, acceptance criteria, attachments, and links.
2. `listJiraIssueComments` picks up decisions made in comments. A later comment overrides the description.
3. `getConfluenceContent` reads each linked Confluence page. Use `searchConfluence` with the Jira key when the card has no link.
4. Build a numbered list, R1, R2, and so on, and give each one a source link.

## 3. Design read

1. `create_session` with the `fileKey`.
2. `get_metadata` for the frame tree in scope.
3. `get_screenshot` for each top-level frame.
4. `get_variable_defs` to see which variables and styles are bound.
5. `use_figma` reads, in a single call, the fills, text styles, sizes, component properties, and variant names that the checks need. Read only. No writes yet.

## 4. Checks

Run only the checks the user kept.

- **Requirements.** Each R gets a status: Done, Partial, Missing, or Unclear. Each Done or Partial status links the frame that answers it. Anything designed that no requirement asks for is listed as Not asked.
- **Accessibility.** Use [references/accessibility.md](references/accessibility.md). Compute contrast from fill values, not from screenshots.
- **States.** Use [references/states.md](references/states.md). When it is unclear whether a state exists, ask instead of guessing.
- **Heuristics.** Use [references/heuristics.md](references/heuristics.md) for a short Nielsen pass.
- **Design system.** Flag hard-coded colors, text without a text style, spacing without variables, and detached instances.
- **Content.** Flag lorem ipsum, placeholder copy, mixed capitalization, and copy that differs from the spec.
- **Handoff.** Flag default layer names (`Frame 12`), missing auto layout on lists and stacks, flows without prototype links, and screens without developer notes.
- **Edge-case data.** Check long names, large numbers, text that grows about 30% in translation, one item versus many, and RTL when the spec mentions it.

Severity for each finding is blocker, major, or minor. The rules are in [references/heuristics.md](references/heuristics.md).

## 5. Preview

Post a short summary in chat. Include a score per area, the counts by severity, the Missing and Unclear requirements, and the missing states.

Then ask with AskQuestion:

- Write the review to Figma.
- Change something first.
- Stop without writing anything to Figma.

## 6. Write to Figma

Follow [references/figma-report.md](references/figma-report.md). Create a `Design review / <JIRA-KEY> / <YYYY-MM-DD>` section to the right of the reviewed frames. It contains the summary, the requirement checklist, numbered pins with finding cards, and dashed placeholders for missing states.

If a review section for the same Jira key already exists, compare the two first. Mark each old finding as Fixed or Still open, then replace the old section.

## 7. Questions for the PM

Gather every Unclear requirement into a list the user can paste into Jira. Show it in chat. Do not post it.

## Rules

- Never write to Jira or Confluence.
- Never edit, move, or delete design layers. Write only inside the review section.
- Never copy tokens, credentials, or personal data into review frames.
- Contrast taken from screenshots is an estimate. Say so when no fill value is available.
