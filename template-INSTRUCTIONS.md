# {{SYSTEM_NAME}} — Agentic Process Instructions

> **Orchestration layer.** This document defines how the `{{SYSTEM_NAME}}` agent system operates: which agents exist, how they are invoked, how they interact, and how to extend the system with new agents.
>
> **Owner**: {{GOVERNANCE_OWNER}}  
> **Created**: {{YYYY-MM-DD}}  
> **Last updated**: {{YYYY-MM-DD}}

---

## System Overview

`{{SYSTEM_NAME}}` is a multi-agent system. Each agent is a focused, scoped specialist that produces a defined deliverable. Agents do not chain themselves — orchestration is the caller's responsibility.

| Document type | Purpose | Location |
|---|---|---|
| **Agent** | Defines role, scope, constraints, and output for one agent | `.github/agents/{{AGENT_NAME}}.md` |
| **Skill** (`SKILL.md`) | Step-by-step execution procedure | `.github/skills/{{AGENT_NAME}}/SKILL.md` |
| **Standards** (`STANDARDS.md`) | Output templates, syntax rules, validation checklists | `.github/skills/{{AGENT_NAME}}/STANDARDS.md` |
| **Core Standards** | Tier 1 universal rules all agents inherit | `.github/standards/core-standards.md` |

### Document Authority Hierarchy

```
core-standards.md          (Tier 1 — universal, never contradicted)
  └── STANDARDS.md         (Tier 2 — skill-local, extends Tier 1)
        └── SKILL.md       (Tier 3 — execution procedure, governed by Tier 2)
              └── Agent    (Tier 4 — role/scope definition, invokes Tier 3)
                    └── INSTRUCTIONS.md  (Tier 5 — orchestration metadata, this file)
```

A lower tier may add specificity but must never contradict a higher tier. If conflict exists, the higher tier wins.

---

## Agents in This System

| Agent | Role | Primary trigger |
|---|---|---|
| `{{PREFIX}}-{{CAPABILITY_1}}` | {{One-line role description.}} | {{When to invoke this agent.}} |
| `{{PREFIX}}-{{CAPABILITY_2}}` | {{One-line role description.}} | {{When to invoke this agent.}} |
| `{{PREFIX}}-{{CAPABILITY_3}}` | {{One-line role description.}} | {{When to invoke this agent.}} |
| `{{PREFIX}}-{{CAPABILITY_4}}` | {{One-line role description.}} | {{When to invoke this agent.}} |

---

## How to Invoke an Agent

Every agent follows this execution protocol. Do not invoke an agent unless the caller is prepared to provide an argument matching the agent's `argument-hint`.

1. **Read the agent definition** — load `.github/agents/{{AGENT_NAME}}.md` to confirm scope and constraints.
2. **Read SKILL.md** — load `.github/skills/{{AGENT_NAME}}/SKILL.md` for the step-by-step procedure.
3. **Read STANDARDS.md** — load `.github/skills/{{AGENT_NAME}}/STANDARDS.md` for output templates and validation rules.
4. **Read core-standards.md** — load `.github/standards/core-standards.md` for universal evidence and file operation rules.
5. **Execute all steps in order** — do not skip, reorder, or summarise.
6. **Validate output** — run the File Creation Validation Checklist from STANDARDS.md before completing.
7. **Write artifacts to disk** — confirm each file was written at the exact expected path.

---

## Agent Interaction Model

Agents are **non-recursive** by default:

- An agent produces its designated deliverable and surfaces a `Handoff Note` for any out-of-scope findings.
- An agent does **not** invoke another agent directly.
- An agent does **not** produce another agent's deliverable, even if the work seems adjacent.
- **Orchestration** — chaining agents in a workflow — is the caller's responsibility, not the agent's.

### Handoff Note Format

When an agent finds something outside its scope, it appends this block to its output before stopping:

```markdown
## Handoff Note
**Target agent**: `{{PREFIX}}-{{TARGET_CAPABILITY}}`
**Finding**: {{One-sentence description of the out-of-scope finding.}}
```

---

## Creating a New Agent

Follow these steps in order. Do not activate an agent until all five steps are complete.

1. **Copy `template-AGENT.md`** → `.github/agents/{{NEW_AGENT_NAME}}.md` and fill every `{{PLACEHOLDER}}`.
2. **Create `.github/skills/{{NEW_AGENT_NAME}}/SKILL.md`** from `template-SKILL.md` — fill every `{{PLACEHOLDER}}`.
3. **Create `.github/skills/{{NEW_AGENT_NAME}}/STANDARDS.md`** from `template-STANDARDS.md` — fill every `{{PLACEHOLDER}}`.
4. **Add the agent to the table** in this INSTRUCTIONS.md under "Agents in This System".
5. **Validate cross-references** — AGENT.md → SKILL.md → STANDARDS.md → core-standards.md links must all resolve.

### Naming Conventions

| Item | Convention | Example |
|---|---|---|
| Agent name | `{{PREFIX}}-{{capability}}` — all lowercase, hyphen-separated | `cognia-arch` |
| Skill directory | Match agent name exactly | `skills/cognia-arch/` |
| Output folder | Short, lowercase noun | `cognia/` |
| Output files | `{project_name}-{{capability}}.md` / `.html` | `myapp-architecture.md` |
| Design-time placeholder | `{{UPPER_SNAKE_CASE}}` double-brace — fill when instantiating the template | `{{AGENT_NAME}}` |
| Runtime variable | `{lower_case}` single-brace — filled by the caller at invocation | `{project_name}` |

Both placeholder tiers must be fully resolved before an agent is considered ready. See `core-standards.md §9` for the full convention.

---

## Deprecating an Agent

1. Remove the agent row from the table in this INSTRUCTIONS.md.
2. Move `.github/agents/{{AGENT_NAME}}.md` to `.github/agents/deprecated/`.
3. Move `.github/skills/{{AGENT_NAME}}/` to `.github/skills/deprecated/`.
4. Do not delete historical output files produced by the agent — archive them.

---

## Governance

| Change type | Approval required from |
|---|---|
| Edits to `core-standards.md` (Tier 1) | {{GOVERNANCE_OWNER}} |
| New agent (Tier 3 + Tier 2 documents) | {{TEAM_LEAD}} |
| Changes to an existing SKILL.md or STANDARDS.md | {{AGENT_OWNER}} |
| Changes to INSTRUCTIONS.md | {{GOVERNANCE_OWNER}} |

All changes to Tier 1 or Tier 2 documents must be reviewed before agents use the updated versions.
