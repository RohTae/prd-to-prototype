---
description: Phase 2 — Write the PRD based on research outputs.
---

# Phase 2: PRD

Prerequisite: Verify `/outputs/01-research/` contains research deliverables.
If missing, instruct user to run `/research` first.

## Execution
Delegate to the prd-writer subagent:
- Reference all research outputs to write the PRD
- Classify features using MoSCoW
- Generate User Flow diagrams
- Define success metrics (KPIs)

## Completion Criteria
`/outputs/02-prd/` must contain: PRD.md, user-flows.md, feature-matrix.md

## Next Step
Run `/review 2` to validate PRD quality, then `/ia`.
