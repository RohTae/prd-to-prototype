---
description: Phase 4 — Generate per-screen HTML wireframes based on the IA design.
---

# Phase 4: Wireframe

Prerequisite: Verify `/outputs/03-ia/screen-inventory.md` exists.

## Execution
Delegate to the wireframer subagent:
- Convert each screen to a standalone HTML wireframe
- Grayscale structural layout with annotation overlays
- Link screens via `<a href>` for browser-based navigation
- Identify shared patterns

## Completion Criteria
`/outputs/04-wireframe/` must contain:
- index.html (wireframe hub — links to all screens)
- S-{NNN}-{screen-name}.html files (opens directly in browser)
- shared-patterns.md (with HTML snippets)
- wireframe-index.md

## Next Step
Run `/review 4`, then `/prototype`.
