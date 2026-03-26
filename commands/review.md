---
description: Validate a Phase's deliverables against quality checklists. Usage — /review {phase_number} (e.g., /review 2)
---

# Quality Gate Review

Delegates to the qa-reviewer subagent to validate the specified Phase.

## Input
$ARGUMENTS — Phase number (1-6) or "all"

Phase mapping:
- 1 → /outputs/01-research/
- 2 → /outputs/02-prd/
- 3 → /outputs/03-ia/
- 4 → /outputs/04-wireframe/
- 5 → /outputs/05-design-system/
- 6 → /outputs/06-prototype/

## Execution
The qa-reviewer subagent will:
- Run phase-specific checklist validation
- Verify traceability to prior Phase outputs
- Issue PASS / CONDITIONAL PASS / FAIL verdict

## Output
Review report saved to `/outputs/{phase}/REVIEW.md`

## On FAIL
Review the FAIL items and request corrections from the relevant subagent.
Re-run `/review {phase}` after fixes.
