---
title: "Phase Review Checklist"
phase: all
created: YYYY-MM-DD
---

# Review Checklist — Phase {N}

## Review Info
- **Reviewer**: qa-reviewer agent
- **Date**: YYYY-MM-DD
- **Phase**: {N}
- **Verdict**: PASS / CONDITIONAL PASS / FAIL

---

## 1. File Existence Check
| Required File | Exists? | Notes |
|---------------|---------|-------|
| [filename] | ✅ / ❌ | |

---

## 2. Quality Checklist
| # | Criterion | Status | Evidence / Notes |
|---|-----------|--------|-----------------|
| 1 | [check item] | ✅ / ❌ / ⚠️ | [specific location or description] |

---

## 3. Traceability Check
| Source (Previous Phase) | Target (Current Phase) | Linked? | Notes |
|------------------------|----------------------|---------|-------|
| [prior Phase item] | [current Phase item] | ✅ / ❌ | |

---

## 4. Critical Issues (FAIL items)
> "None" if no FAIL items

### Issue 1: [Title]
- **File**: [filename:line_number]
- **Problem**: [description]
- **Impact**: [what this affects]
- **Fix Direction**: [suggested resolution]

---

## 5. Warnings & Recommendations
> "None" if no warnings

### Recommendation 1: [Title]
- **File**: [filename]
- **Current**: [current state]
- **Suggested**: [improvement]
- **Priority**: High / Medium / Low

---

## 6. Summary
[2-3 sentence overall assessment]

**Next Action**: [If PASS → next Phase guidance / If FAIL → items to fix]
