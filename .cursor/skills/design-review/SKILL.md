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

Load the `figma-use` skill before any `use_figma` call. Reply in the user's language.

Start the review in the same turn the user gives a Jira key and a Figma URL. Do not ask which checks to run, which frames to include, or to confirm the links. Run every check. The only question comes after the summary, before writing to Figma.

Ask only when something required is missing, and ask for that one thing in a sentence:

- No Jira key and no requirements pasted in the chat.
- No Figma URL.
- A Figma URL with no `node-id` in a file that has more than one page.

## 1. Inputs

Take the Jira key from a key like `AP-3966` or from a `atlassian.net/browse/` URL. Take the Figma file from `figma.com/design/:fileKey/:name?node-id=1-2`, which gives `fileKey` and node `1:2`. For a branch URL, use the branch key as the file key.

Scope comes from the node:

- A page: every frame on that page, except sections named `Design review`.
- A section: the frames inside it.
- A frame: that frame.

A check the user names as off stays off. Anything they don't mention runs.

Do the requirements, the design read, and the checks without stopping. A doubt becomes an Unclear item in the report, not a question that pauses the review.

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

- **Requirements.** Each R gets a status: Done, Partial, Missing, or Unclear. Each Done or Partial status links the frame that answers it. Anything designed that no requirement asks for is listed as Not asked.
- **Accessibility.** Use [references/accessibility.md](references/accessibility.md). Compute contrast from fill values, not from screenshots.
- **States.** Use [references/states.md](references/states.md). When it is unclear whether a state exists, mark it Unclear and continue.
- **Heuristics.** Use [references/heuristics.md](references/heuristics.md) for a short Nielsen pass.
- **Design system.** Flag hard-coded colors, text without a text style, spacing without variables, and detached instances.
- **Content.** Flag lorem ipsum, placeholder copy, mixed capitalization, and copy that differs from the spec.
- **Handoff.** Flag default layer names (`Frame 12`), missing auto layout on lists and stacks, flows without prototype links, and screens without developer notes.
- **Edge-case data.** Check long names, large numbers, text that grows about 30% in translation, one item versus many, and RTL when the spec mentions it.

Severity for each finding is blocker, major, or minor. The rules are in [references/heuristics.md](references/heuristics.md).

## 5. Preview

Post the summary in chat: a score per area, the counts by severity, and the findings, with the blockers first. Keep each finding to what is wrong, why, and the fix.

Then ask one question: write this into the Figma file? Wait for the answer. A change they ask for updates the summary. Writing nothing leaves the review in the chat.

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
