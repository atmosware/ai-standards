# ai-standards

Org-wide template library for building standardized AI agents, skills, and instructions across all projects.

---

## Table of Contents

- [Why This Exists](#why-this-exists)
- [Repository Contents](#repository-contents)
- [Instructions vs Skills vs Agents](#instructions-vs-skills-vs-agents)
- [Document Authority Hierarchy](#document-authority-hierarchy)
- [How to Add a New Agent](#how-to-add-a-new-agent)
- [Key Rules (from `core-standards.md`)](#key-rules-from-core-standardsmd)
- [Expected Structure in Consuming Projects](#expected-structure-in-consuming-projects)
- [Governance](#governance)

---

## Why This Exists

Agent development was inconsistent across projects — different structure, different evidence conventions, different output formats. This repo is the single source of truth that every team copies from, so every agent follows the same rules regardless of which project it lives in.

**Projects that inherit these standards:**

| Project | Type |
|---|---|
| `cognia-agents` | Read-only analysis / audit agents |
| `praxia-agents` | Action agents with human approval gates |
| `legacy-modernization-orchestrator` | Multi-phase orchestration (13 phases) |

---

## Repository Contents

| File | Purpose |
|---|---|
| `core-standards.md` | **Tier 1** — Universal rules every agent inherits without exception |
| `template-AGENT.md` | Base template for agent definition files (`.github/agents/*.md`) |
| `template-AGENT-backend.md` | Pre-filled agent template for backend teams (endpoints, services, DB, auth, integrations) |
| `template-AGENT-frontend.md` | Pre-filled agent template for frontend teams (pages, components, state, API, bundle) |
| `template-AGENT-ios.md` | Pre-filled agent template for iOS teams (screens, navigation, networking, Swift/ObjC, App Store) |
| `template-AGENT-android.md` | Pre-filled agent template for Android teams (screens, navigation, networking, Kotlin/Java, Play Store) |
| `template-AGENT-action.md` | Template for action agents with Phase 1 Propose / Phase 2 Execute human-approval gate (praxia-style) |
| `template-SKILL.md` | Template for step-by-step execution procedures (`SKILL.md`) |
| `template-STANDARDS.md` | Template for output templates and validation checklists (`STANDARDS.md`) |
| `template-INSTRUCTIONS.md` | Template for system-level orchestration documents (`INSTRUCTIONS.md`) |

---

## Instructions vs Skills vs Agents

### Instructions

**What they are:** Plain text directives that shape how an AI model behaves — its tone, constraints, persona, output format, domain focus, etc. They live in the system prompt.

**Think of them as:** The rulebook or job description given to the model before it starts working.

**When to use:**

- You want consistent behavior across all interactions (e.g., "always respond in Turkish", "never discuss competitors")
- You're defining a persona or role (e.g., "you are a senior Java developer")
- You need to constrain scope (e.g., "only answer questions about our product")
- Simple, stateless tasks where the model just needs context to do its job well

**Example:** A customer support bot told to always be polite, escalate billing issues, and never promise refunds.

### Skills

**What they are:** Reusable, packaged capabilities — typically a combination of a prompt template, context, and sometimes tool access — that teach the model how to do a specific task well. In some frameworks (like the one you're working in), skills are `.md` files with step-by-step instructions optimized for a particular domain.

**Think of them as:** Standard operating procedures (SOPs) or specialized training modules the model can load on demand.

**When to use:**

- The task is recurring and well-defined (e.g., "create a `.docx` file", "read a PDF", "build a frontend component")
- Quality and consistency matter — you've invested effort in figuring out the right way to do something and want to reuse that
- You want to compose capabilities (e.g., read a PDF skill + summarize skill together)
- The task has domain-specific nuances the base model might get wrong without guidance

**Example:** A docx skill that knows exactly which Python library to use, how to handle fonts, tables, and headers correctly in Word files — so you don't have to re-figure that out every time.

### Agents

**What they are:** Autonomous systems where an AI model can take sequences of actions, use tools, make decisions, and loop until a goal is achieved — rather than just generating a single response.

**Think of them as:** An employee who doesn't just answer a question but actually does the work — browsing the web, writing files, calling APIs, running code, checking results, and correcting course.

**When to use:**

- The task requires multiple steps that depend on each other (e.g., "research this topic, write a report, save it as PDF")
- You need tool use: file system, APIs, databases, web search, code execution
- The path to the answer isn't known upfront — the model needs to reason and adapt
- Long-horizon tasks where intermediate results influence next steps

**Example:** An agent that receives "analyze our OpenShift deployment logs, identify the root cause, and draft a fix recommendation" — it reads logs, searches docs, reasons about the failure, and writes a report.

### How They Relate

```
Instructions  ──▶  shape the agent's/model's behavior at all times
Skills        ──▶  give it specialized know-how for specific tasks
Agents        ──▶  execute multi-step work using instructions + skills + tools
```

A well-designed system combines all three: instructions set the foundation, skills are loaded when a specific task type is detected, and agents orchestrate everything when the work requires real autonomy and action.

---

## Document Authority Hierarchy

Every consuming project uses a five-tier authority model. Lower tiers may add specificity but must never contradict a higher tier. When conflict exists, the higher tier wins.

```
core-standards.md          (Tier 1 — universal, never contradicted)
  └── STANDARDS.md         (Tier 2 — skill-local, extends Tier 1)
        └── SKILL.md       (Tier 3 — step-by-step execution procedure)
              └── Agent    (Tier 4 — role/scope definition, invokes Tier 3)
                    └── INSTRUCTIONS.md  (Tier 5 — orchestration metadata, caller-owned)
```

---

## How to Add a New Agent

Do not activate an agent until all five steps are complete.

1. **Copy `template-AGENT.md`** → `.github/agents/{{AGENT_NAME}}.agent.md` and fill every `{{PLACEHOLDER}}`.
2. **Create `.github/skills/{{AGENT_NAME}}/SKILL.md`** from `template-SKILL.md` — fill every `{{PLACEHOLDER}}`.
3. **Create `.github/skills/{{AGENT_NAME}}/STANDARDS.md`** from `template-STANDARDS.md` — fill every `{{PLACEHOLDER}}`.
4. **Add the agent row** to the INSTRUCTIONS.md table under "Agents in This System".
5. **Validate cross-references** — AGENT.md → SKILL.md → STANDARDS.md → core-standards.md links must all resolve.

### Naming Conventions

| Item | Convention | Example |
|---|---|---|
| Agent name | `{prefix}-{capability}` — lowercase, hyphen-separated | `cognia-arch` |
| Skill directory | Match agent name exactly | `skills/cognia-arch/` |
| Output folder | Short, lowercase noun | `cognia/` |
| Output files | `{project_name}-{capability}.md` / `.html` | `myapp-architecture.md` |
| Placeholder variables | `{{UPPER_SNAKE_CASE}}` double-brace | `{{AGENT_NAME}}` |

---

## Key Rules (from `core-standards.md`)

These apply to every agent in every project:

- **Evidence tagging** — every material claim must be tagged `Confirmed` (file-evidenced), `Inferred` (indirect evidence), or `Not found in scanned files`. Never guess.
- **File operations** — always overwrite output files completely. Never append.
- **Scope enforcement** — if a finding is out of scope, write a `Handoff Note` and stop. Do not produce another agent's deliverable.
- **Step compliance** — never skip, reorder, or summarise steps defined in a SKILL.md.
- **Security** — never write credentials, secrets, API keys, or PII to any output file.

---

## Expected Structure in Consuming Projects

Each project that adopts these standards should maintain this layout:

```
.github/
  agents/              # Canonical agent definitions (filled templates)
    {agent-name}.agent.md
  skills/
    {agent-name}/
      SKILL.md         # Step-by-step procedure
      STANDARDS.md     # Output templates and validation checklists
  standards/
    core.md            # Copied from this repo (Tier 1)
  instructions/
    INSTRUCTIONS.md    # System orchestration document
.claude/
  agents/              # Thin Claude Code wrapper — redirects to .github/agents/
```

---

## Governance

| Change type | Approval required from |
|---|---|
| Edits to `core-standards.md` (Tier 1) | Governance owner |
| New template | Governance owner |
| Changes to an existing template | Template owner |

All changes to Tier 1 documents must be reviewed before downstream agents consume the updated version.
