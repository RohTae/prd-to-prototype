---
description: Phase 5+6 — Build design system + interactive prototype as a single HTML file.
---

# Phase 5-6: Design System + Prototype

Prerequisites:
- `/outputs/04-wireframe/*.html` wireframe files exist
- `/outputs/04-wireframe/shared-patterns.md` exists

## Execution — Two Sequential Steps

### Step A: Design System
Delegate to design-system-engineer subagent:
- Extract shared patterns into components
- Define design tokens (colors, typography, spacing)
- Build component library as browsable HTML

Verify: `/outputs/05-design-system/component-library.html` exists

### Step B: Prototype
After design system is complete, delegate to prototype-builder subagent:
- Assemble components into interactive pages
- Implement user-flow-based screen transitions
- Add mock data and interactions
- Include demo controls

## Completion Criteria
`/outputs/05-design-system/`:
- design-tokens.html, component-library.html, tailwind-config.js, component-catalog.md

`/outputs/06-prototype/`:
- prototype.html (single file — double-click to run in browser)
- prototype-guide.md

## Next Step
Run `/review 6` for final validation.
