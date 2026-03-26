---
title: "Screen Inventory"
phase: 3
created: YYYY-MM-DD
status: draft
depends_on:
  - "outputs/02-prd/PRD.md"
  - "outputs/02-prd/feature-matrix.md"
---

# Screen Inventory

## Overview
| Screen ID | Screen Name | Category | Priority | Status |
|-----------|-------------|----------|----------|--------|
| S-001 | | Auth / Core / Settings / Sub | High/Med/Low | Defined |

---

## Screen Details

### S-001: [Screen Name]

**Purpose**: [Why this screen exists — 1 sentence]

**User Goal**: [What the user is trying to accomplish here]

**Key Elements**:
- [ ] [UI element 1 — e.g., Search bar]
- [ ] [UI element 2 — e.g., Card list]
- [ ] [UI element 3 — e.g., FAB button]

**Primary Action**: [Main CTA — e.g., "Add New Item" button]

**Navigation**:
- Entry Points: [How users arrive here]
  - S-000 → "Tab click"
  - S-003 → "Back button"
- Exit Points: [Where users go next]
  - "Item click" → S-002
  - "Add button" → S-004

**State Variations**:
| State | Trigger | Display |
|-------|---------|---------|
| Default | Data exists | Card list displayed |
| Empty | No data | Empty state illustration + CTA |
| Loading | Data loading | Skeleton UI |
| Error | API failure | Error message + retry |

**Related PRD Features**: F-001, F-003

**Notes**: [Additional considerations]

---

### S-002: [Next Screen]
[Repeat format above]
