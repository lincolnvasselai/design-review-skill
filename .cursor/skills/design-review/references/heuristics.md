# Heuristics and severity

## Nielsen pass

Keep it short. Report only clear issues and tag each one with its heuristic number.

1. Visibility of system status: loading, progress, saved, and sent feedback.
2. Match with the real world: user language, not internal terms.
3. User control and freedom: cancel, back, undo, close.
4. Consistency and standards: the same action looks and is named the same everywhere.
5. Error prevention: confirmations on destructive actions, constraints on inputs.
6. Recognition rather than recall: visible options, no hidden codes.
7. Flexibility and efficiency: shortcuts, defaults, bulk actions where the spec expects heavy use.
8. Aesthetic and minimalist design: no competing primary actions, clear hierarchy.
9. Help users recover from errors: plain message, cause, and the way out.
10. Help and documentation: tooltips or help links where the task is complex.

## Severity

| Severity | Use when |
|---|---|
| blocker | A requirement is Missing, a WCAG AA failure blocks a task (unreadable text, no label, color-only error), or a state is missing that breaks the flow (no error state on a form). |
| major | A requirement is Partial, there is a WCAG AA failure on secondary content, an expected state is missing (hover, focus, empty), or a heuristic issue causes real confusion. |
| minor | A recommendation and not a rule, a cosmetic inconsistency, naming or handoff hygiene, or a design system drift with no visible change. |

## Scores

Each area gets a score from 0 to 100: `100 - 25 × blockers - 10 × majors - 2 × minors`, with a floor of 0. Requirements use the share of R items marked Done, with Partial counted as half.
