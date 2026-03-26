---
name: quality-gate
description: Auto-validates prerequisites when transitioning between pipeline Phases. Checks prior Phase output existence and REVIEW.md PASS status. Triggers automatically on Phase transitions, next-step progression, and subagent delegation.
---

# Quality Gate — Auto-Validation Rules

This skill fires automatically during Phase transitions to validate prerequisites.

## Phase Dependency Map

```
Phase 2 (PRD)       → Phase 1 required: 01-research/{research-report,personas,competitive-analysis,key-insights}.md
Phase 3 (IA)        → Phase 2 required: 02-prd/{PRD,user-flows,feature-matrix}.md
Phase 4 (Wireframe) → Phase 3 required: 03-ia/{screen-inventory,ia-summary,navigation-structure,refined-user-flows}.md
Phase 5 (Design)    → Phase 4 required: 04-wireframe/{shared-patterns}.md + at least one .html file
Phase 6 (Prototype) → Phase 5 required: 05-design-system/{component-library}.html + {tailwind-config}.js
```

## Validation Process

Before starting Phase N:

1. **File Existence Check**: Verify all required files from prior Phase exist per the dependency map above.
2. **Review Check (Recommended)**: Verify prior Phase's REVIEW.md exists and Verdict is PASS or CONDITIONAL PASS.
   - No REVIEW.md: Show warning, allow to proceed ("⚠️ Phase {N-1} has not been reviewed. Running /review {N-1} is recommended.")
   - FAIL verdict: Block. "❌ Phase {N-1} review is FAIL. Fix issues and re-review before proceeding."

3. **Result**:
   - ✅ All conditions met → Proceed silently
   - ⚠️ Review incomplete → Warn and allow
   - ❌ Missing files or FAIL → Block with specific missing items listed

## Exceptions
- Phase 1 (Research) has no prerequisites. Only `/briefs/product-brief.md` must exist.
- `/kickoff` command bypasses this validation (initial setup).
