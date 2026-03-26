# AI Agent Pipeline: PRD → Wireframe → Prototype
## Multi-Agent Product Development System for Claude Code

> Built on 2026 best practices: Claude Code Agent Teams + Subagents + Skills

---

## 📊 Research Summary: 2026 Multi-Agent Trends

### Three Key Shifts

**1. Agent Teams (Native Multi-Agent)**
- Shipped with Opus 4.6 in February 2026 as an experimental feature
- Unlike subagents, teammates can **communicate directly** (P2P mailbox system)
- Each agent operates in its own context window + Git worktree
- Real-time monitoring via tmux split panes

**2. Skill + Subagent + MCP Trinity**
- Skill = expertise (what to do)
- Subagent = context boundary (keeps main context clean)
- MCP = external tool access (Figma, GitHub, etc.)
- Combining all three breaks the "prompt engineering hamster wheel"

**3. Prototype > PRD Paradigm Shift**
- 2026 trend: Agents that produce prototypes are more valuable than agents that write documents
- PRDs are still necessary, but the goal is to reach a clickable prototype as fast as possible
- Plan → Build two-phase mode has become standard

### Implementation Approach Comparison

| Approach | Strengths | Weaknesses | Best For |
|----------|-----------|------------|----------|
| **Slash Commands** | Explicit, repeatable | Manual invocation | Fixed-order pipelines |
| **Subagents** | Context isolation, tool restrictions | No inter-agent communication | Independent single tasks |
| **Agent Teams** | P2P messaging, parallel work | High token usage, experimental | 3+ specialists collaborating |
| **Skills** | Auto-invocation, reusable | Runs in main context | Recurring domain knowledge |

### Recommended Architecture: Hybrid Approach

```
Phase 1-2 (sequential) → Slash Commands + Subagents
Phase 3 (parallelizable) → Agent Teams (UI + Component work in parallel)
Overall quality control  → Skills (auto-invoked QA rules)
```

### Prompt Optimization Principles (Based on 2026 Best Practices)

1. **Contract format**: Structuring each agent prompt as Role/Process/Output/Quality Criteria/Constraints yields consistent quality.
2. **Personality section**: Directives like "be critical" and "be honest" override the LLM's default agreeableness.
3. **Explicit prerequisites**: "Stop if this file doesn't exist" prevents Phase contamination.
4. **Context isolation**: Heavy file-reading tasks must go to subagents to keep the main context clean.
5. **Progressive disclosure**: Skills only load name/description first; the body loads on demand, saving tokens.

---

## 📁 Project Structure

```
project-root/
├── CLAUDE.md                          # Orchestrator (global context)
├── .claude/
│   ├── agents/                        # Subagent definitions
│   │   ├── researcher.md
│   │   ├── prd-writer.md
│   │   ├── ia-strategist.md
│   │   ├── wireframer.md
│   │   ├── design-system-engineer.md
│   │   ├── prototype-builder.md
│   │   └── qa-reviewer.md
│   ├── commands/                      # Slash Commands
│   │   ├── kickoff.md                 # /kickoff — Start pipeline
│   │   ├── research.md                # /research
│   │   ├── prd.md                     # /prd
│   │   ├── ia.md                      # /ia
│   │   ├── wireframe.md               # /wireframe
│   │   ├── prototype.md               # /prototype
│   │   └── review.md                  # /review
│   └── skills/                        # Auto-invocation Skills
│       ├── quality-gate/
│       │   └── SKILL.md
│       └── design-conventions/
│           └── SKILL.md
├── templates/                         # Deliverable templates
│   ├── prd-template.md
│   ├── persona-template.md
│   ├── screen-inventory-template.md
│   └── review-checklist.md
├── outputs/                           # Per-Phase deliverables
│   ├── 01-research/
│   ├── 02-prd/
│   ├── 03-ia/
│   ├── 04-wireframe/
│   ├── 05-design-system/
│   └── 06-prototype/
└── briefs/
    └── product-brief.md
```

---

## 🛠 Installation

```bash
# 1. Extract the archive into your project root
tar xzf agent-pipeline-system.tar.gz

# 2. Run the installer (renames claude-config → .claude)
chmod +x install.sh && ./install.sh

# 3. Verify
ls -la .claude/
# Should show: agents/  commands/  skills/
```

The archive ships `claude-config/` (visible folder) instead of `.claude/` (hidden folder) because most OS file explorers hide dot-prefixed directories. The `install.sh` script renames it to `.claude/` which Claude Code requires.

---

## 🚀 Usage

### Basic Mode: Slash Commands (Sequential)

```bash
# 0. Start pipeline
/kickoff "AI-powered habit tracker mobile app for professionals"

# 1. Research
/research

# 2. Write PRD
/prd

# 3. Review PRD
/review 2

# 4. Information Architecture
/ia

# 5. Wireframes
/wireframe

# 6. Review wireframes
/review 4

# 7. Design system + prototype
/prototype

# 8. Final review
/review 6
```

### Advanced Mode: Agent Teams (Parallel)

Enable Agent Teams for parallel Phase 4-5 execution:

```bash
# Setup (once)
# Add to settings.json:
# "CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS": "1"

# After IA is complete, run wireframe + design system in parallel:
"Spawn a team of 3 agents:
 1. wireframer — generate wireframes from screen-inventory
 2. design-system-engineer — build components from shared-patterns
 3. qa-reviewer — review each as they complete

Once wireframe and design system are both done, hand off to prototype-builder."
```

---

## 🧠 Agent Design Strategy

### Agent Summary

| Agent | Role | Key Personality | Tools | Differentiator |
|-------|------|----------------|-------|----------------|
| **Researcher** | Market/user research | Critical, skeptical | Read,Grep,Glob,Bash,WebFetch | Anti-Persona defines target boundary |
| **PRD Writer** | Product requirements | Clear, measurement-focused | Read,Grep,Glob,Bash | Given/When/Then + Edge Cases mandatory |
| **IA Strategist** | Info architecture & screens | User-centric, simplicity | Read,Grep,Glob,Bash | 3-click rule + State Variations |
| **Wireframer** | Structural wireframes | Pragmatic, layout-obsessed | Read,Grep,Glob,Bash,Edit | Grayscale + annotation system |
| **Design System Engineer** | Component library | Consistency-obsessed, DRY | Read,Grep,Glob,Bash,Edit | Atomic → Molecular hierarchy |
| **Prototype Builder** | Interactive prototype | Speed-focused, feel-focused | Read,Grep,Glob,Bash,Edit | Demo mode + realistic mock data |
| **QA Reviewer** | Quality gate | Meticulous, specific, constructive | Read,Grep,Glob,Bash | Traceability verification |

### Prompt Structure Pattern (Common to All Agents)

```
--- (YAML frontmatter)
name / description / tools / model
---

# Role           ← "You are a ~" (grants expertise)
# Personality    ← Overrides default LLM agreeableness
# Input          ← Prerequisites + reference files (hard stop if missing)
# Process        ← Step 1/2/3... concrete execution order
# Output         ← Exact file paths + filenames
# Quality Criteria ← Self-validation checklist
# Constraints    ← What NOT to do (boundary setting)
```

### Design Rationale per Agent

**1. Researcher — Why "critical personality"?**
LLMs default to positive responses, risking failure to identify weaknesses in an idea. Explicit instructions like "be critical" and "distinguish assumptions from facts" correct this bias. The Anti-Persona requirement serves the same purpose.

**2. PRD Writer — Why enforce "Given/When/Then"?**
Natural language requirements are ambiguous, and ambiguity compounds downstream. Structured Acceptance Criteria let the IA agent map screens precisely and give the QA agent verifiable standards.

**3. IA Strategist — Why the "Screen ID" system?**
This is the backbone of cross-Phase traceability. PRD F-001 → IA S-001 → Wireframe S-001-home.html. Without this ID chain, the QA agent cannot verify completeness.

**4. Wireframer — Why "grayscale enforced"?**
When color is present, stakeholders give color feedback instead of layout feedback. Removing visual elements intentionally focuses reviews on structural issues. Only annotation blue is allowed to visually separate interaction notes from content.

**5. Design System Engineer — Why after Wireframe?**
Building a design system without wireframes produces "components that might exist" rather than "components that are actually needed." Extracting from shared-patterns.md ensures you build exactly what's required.

**6. Prototype Builder — Why "demo mode"?**
The prototype's purpose is user testing. Toggling between Empty/Loaded/Error states enables scenario-based testing. This is what separates a prototype from a static mockup.

**7. QA Reviewer — Why "traceability verification"?**
The most common failure mode is "insights from Phase 1 not reflected in Phase 4." The Traceability Check structurally prevents this drift.

---

## 📎 References

- [Claude Code Subagents Docs](https://code.claude.com/docs/en/sub-agents)
- [Claude Code Agent Teams Docs](https://code.claude.com/docs/en/agent-teams)
- [Claude Code Best Practices](https://code.claude.com/docs/en/best-practices)
- [Claude Prompting Best Practices](https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/claude-prompting-best-practices)
