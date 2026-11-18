# Design review skill

Reviews a Figma design against its Jira card and the Confluence specs linked to it.

The skill lives in `.cursor/skills/design-review`. Open this repo in Cursor and ask it to review a design. Give it the Jira key and the Figma URL. It checks:

- **Requirements:** whether everything the card and spec ask for was designed
- **Accessibility:** WCAG 2.2 AA contrast, target size, labels, focus, and color-only meaning
- **States:** hover, focus, disabled, loading, empty, error, and more
- **Heuristics:** a short Nielsen pass
- **Design system, content, handoff, and edge-case data**

It shows a summary in chat first. After you confirm, it writes a `Design review / <JIRA-KEY> / <date>` section next to the frames in Figma. The section has scores, a requirement checklist, numbered pins with finding cards, and dashed placeholders for missing states. Running it again marks which findings were fixed.

The skill never edits your design layers and never writes to Jira or Confluence.

## Needs

- The Figma MCP, with edit access to the file
- The Atlassian MCP, for Jira and Confluence

## Share with the team

Clone this repo and open it in Cursor. The skill is available in this project.
