---
description: Start the full product development pipeline. Creates brief and initializes all phases.
argument-hint: "<product idea description>"
---

# Pipeline Kickoff

Collect a product idea from the user and initialize the full pipeline in the current project directory.

## Step 1: Initialize Project Structure

Create all required directories:

```bash
mkdir -p outputs/{01-research,02-prd,03-ia,04-wireframe,05-design-system,06-prototype}
mkdir -p briefs templates
```

## Step 2: Create Templates

Write the following 4 template files into the project's `templates/` directory. These are referenced by pipeline agents during execution.

### File: templates/persona-template.md

Write this file with the following content:

---
title: "User Personas"
phase: 1
created: YYYY-MM-DD
status: draft
---

Primary Persona section: Demographics (Age, Occupation, Tech Savviness, Primary Device), Behavioral Profile (Daily Routine, Current Workaround, Discovery Pattern), Motivations (3 items), Pain Points (3 items with specific situation and impact), Scenario (narrative paragraph), Product Expectations (Must/Nice/Concern).

Secondary Persona: Same format as Primary.

Anti-Persona: Why This Person Is NOT the Target, Demographics, Reaction to This Product, Design Implication.

### File: templates/prd-template.md

Write this file with the following content:

---
title: "[Product Name] — Product Requirements Document"
phase: 2
created: YYYY-MM-DD
status: draft
depends_on:
  - "outputs/01-research/research-report.md"
  - "outputs/01-research/personas.md"
  - "outputs/01-research/competitive-analysis.md"
  - "outputs/01-research/key-insights.md"
---

Sections:
1. Product Overview (Name, Problem Statement, Vision, Target User)
2. Goals & Success Metrics (Business Goals table with KPI/Baseline/Target/Measurement, User Goals same format)
3. Feature Requirements — MoSCoW:
   - Must Have: F-001 format with User Story, Acceptance Criteria (Given/When/Then x3), Edge Cases (x2)
   - Should Have: table with ID/Feature/User Story/Priority Rationale
   - Could Have: table with ID/Feature/Description/Future Consideration
   - Won't Have: table with Feature/Exclusion Reason
4. User Flows (Mermaid flowchart diagrams, 3-5 core flows)
5. Non-Functional Requirements (Performance, Accessibility, Security, Platforms)
6. Technical Constraints & Assumptions (table with Type/Description/Status)
7. Out of Scope (table with Item/Reason)
8. Open Questions (table with #/Question/Owner/Due Date/Decision)

### File: templates/screen-inventory-template.md

Write this file with the following content:

---
title: "Screen Inventory"
phase: 3
created: YYYY-MM-DD
status: draft
depends_on:
  - "outputs/02-prd/PRD.md"
  - "outputs/02-prd/feature-matrix.md"
---

Overview table: Screen ID / Screen Name / Category / Priority / Status

Per screen (S-001 format):
- Purpose (1 sentence)
- User Goal
- Key Elements (checklist)
- Primary Action (main CTA)
- Navigation (Entry Points with source screen IDs, Exit Points with target screen IDs)
- State Variations table: State / Trigger / Display (Default, Empty, Loading, Error)
- Related PRD Features (F-xxx IDs)

### File: templates/review-checklist.md

Write this file with the following content:

---
title: "Phase Review Checklist"
phase: all
created: YYYY-MM-DD
---

Review Info: Reviewer, Date, Phase number, Verdict (PASS / CONDITIONAL PASS / FAIL)

Sections:
1. File Existence Check (table: Required File / Exists? / Notes)
2. Quality Checklist (table: # / Criterion / Status / Evidence)
3. Traceability Check (table: Source Previous Phase / Target Current Phase / Linked? / Notes)
4. Critical Issues — FAIL items (Issue title, File, Problem, Impact, Fix Direction)
5. Warnings & Recommendations (File, Current, Suggested, Priority)
6. Summary (2-3 sentence assessment + Next Action)

## Step 3: Create Project CLAUDE.md

Write a `CLAUDE.md` file in the project root (if one does not already exist) with these pipeline rules:

```markdown
# Product Development Pipeline

## Pipeline Phases
Phase 1: /research  → outputs/01-research/
Phase 2: /prd       → outputs/02-prd/
Phase 3: /ia        → outputs/03-ia/
Phase 4: /wireframe → outputs/04-wireframe/
Phase 5: /prototype → outputs/05-design-system/ + outputs/06-prototype/

## Rules
- Each Phase can only begin when prior Phase outputs exist in outputs/{phase}/
- All deliverables must follow the corresponding template in templates/
- A Phase must pass /review with a PASS verdict before proceeding
- Heavy file-reading tasks must be delegated to subagents

## Verification
- ls outputs/01-research/ → Phase 1 check
- ls outputs/02-prd/ → Phase 2 check
- Check each Phase's REVIEW.md for PASS/FAIL verdict

## Conventions
- Filenames use kebab-case
- Markdown deliverables include YAML frontmatter
- Wireframes are individual .html files (Tailwind CDN, open directly in browser)
- Prototypes are single .html files (all screens + interactions, no build required)
- All diagrams use Mermaid syntax
```

## Step 4: Create Product Brief

Ask the user for the following and write `briefs/product-brief.md`:

1. **One-liner**: What is this product/feature? (1 sentence)
2. **Problem**: Who suffers from what, in what situation?
3. **Target User**: Who is the primary user?
4. **Expected Outcome**: What changes if this product succeeds?
5. **Constraints**: Tech stack, platform, budget, timeline?
6. **References**: Benchmark products, competitors, inspirations?

User input: $ARGUMENTS

If $ARGUMENTS provided, use that content to draft the brief.
If empty, ask the questions one by one.

## Step 5: Show Pipeline Guide

After everything is complete, display:

```
Project initialized!

  briefs/product-brief.md      — Your product idea
  templates/                    — Deliverable templates (4 files)
  outputs/                      — Phase output directories (6 phases)
  CLAUDE.md                     — Pipeline orchestration rules

Execution order:
  1. /research    — Market research & user analysis
  2. /prd         — Write PRD
  3. /review 2    — PRD quality check
  4. /ia          — Information architecture & screen structure
  5. /wireframe   — Generate wireframes
  6. /review 4    — Wireframe quality check
  7. /prototype   — Design system + prototype
  8. /review 6    — Final validation
```
