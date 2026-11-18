# Requirements

## Sources, in priority order

1. Jira comments, newest first. A decision in a comment overrides the description.
2. Jira acceptance criteria field or section.
3. Jira description.
4. Linked Confluence pages: specs, PRDs, flows, copy docs.
5. Jira attachments and linked Figma or Loom items. Note them, but don't count them as requirements unless the text asks for something.

Record conflicts between sources as Unclear, and cite both sources.

## Extracting

- Each requirement is one testable statement. Split "user can filter and sort" into R1 filter and R2 sort.
- Keep the wording close to the source. Do not invent detail.
- Turn Gherkin (`Given / When / Then`) into one R per `Then`.
- Implicit requirements: if the card says "form", the form needs validation and error states. Add these as R items marked `implicit`, and check them under States.
- When the source gives a count ("the seven states"), compare it with the items it lists. A mismatch is an Unclear R.
- Tag each R with its type: `screen`, `component`, `flow`, `copy`, `state`, `breakpoint`, `a11y`, or `data`.

## Format

```
R3 [flow] Show a confirmation step before deleting an address.
   Source: PROJ-123 acceptance criteria #2
```

## Statuses

| Status | Meaning |
|---|---|
| Done | A frame fully answers it. Link the frame. |
| Partial | Some of it is designed. Say what is missing. |
| Missing | No frame answers it. |
| Unclear | The source is vague or conflicting. Add it to the PM questions. |
| Not asked | Designed but not in any source. This is information, not a failure. |

## Mapping to frames

Match a requirement to frames using the frame names, the visible text in screenshots, component names, and prototype flows. When two frames could match, link both. When no frame matches, search the whole page once before marking it Missing.
