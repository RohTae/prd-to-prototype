# prd-to-prototype — Claude Code Plugin

AI agent pipeline that turns a product idea into a clickable prototype.

## Pipeline Overview

```
/kickoff    → Initialize project + product brief
/research   → Phase 1: Market research & user analysis
/prd        → Phase 2: Product Requirements Document
/ia         → Phase 3: Information Architecture & screen inventory
/wireframe  → Phase 4: Per-screen HTML wireframes
/prototype  → Phase 5+6: Design system + interactive prototype
/review N   → Quality gate for Phase N
```

## Architecture

- **7 Subagents**: researcher, prd-writer, ia-strategist, wireframer, design-system-engineer, prototype-builder, qa-reviewer
- **2 Auto-Skills**: quality-gate (phase dependency validation), design-conventions (HTML/CSS/naming rules)
- **7 Commands**: kickoff, research, prd, ia, wireframe, prototype, review

## Phase-Gate Rules

Each Phase can only begin when prior Phase outputs exist. The quality-gate skill enforces this automatically. Commands delegate heavy work to subagents to keep the main context clean.

## Getting Started

Run `/kickoff` in any project directory to initialize the pipeline. This creates:
- `briefs/product-brief.md` — Your product idea
- `templates/` — Deliverable templates (4 files)
- `outputs/` — Phase output directories (6 phases)
- `CLAUDE.md` — Project-level pipeline rules
