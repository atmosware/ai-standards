---
name: {AGENT_NAME}
description: '{{ONE_LINE_DESCRIPTION_USED_FOR_AGENT_SELECTION_MAX_120_CHARS}}'
argument-hint: '{{WHAT_TO_PASS_AS_ARGUMENT_WHEN_INVOKING_THIS_AGENT}}'
---

# {{Agent Display Name}}

## Role
**{{Job Title}}** — {{One or two sentences defining the agent's mission and its primary deliverable. Be specific about what the agent produces, not just what it analyses.}}

## When to Use
- {{Primary trigger: the most common scenario that should invoke this agent.}}
- {{Secondary trigger: a related but distinct scenario.}}
- {{Tertiary trigger: an edge case or less-obvious scenario where this agent adds value.}}

---

## Skill Reference
This agent executes by strictly following every step defined in:

> [`{{AGENT_NAME}}` skill](../skills/{{AGENT_NAME}}/SKILL.md) and [`STANDARDS`](../skills/{{AGENT_NAME}}/STANDARDS.md)

**Do NOT skip, reorder, or summarise steps.** All steps, output format requirements, validation checklists, and file locations are authoritative and must be completed in full.

---

## Core Responsibilities

- **{{Responsibility 1}}**: {{What it means and what the agent produces. One sentence.}}
- **{{Responsibility 2}}**: {{What it means and what the agent produces. One sentence.}}
- **{{Responsibility 3}}**: {{What it means and what the agent produces. One sentence.}}
- **{{Responsibility 4}}**: {{What it means and what the agent produces. One sentence.}}
- **{{Responsibility 5}}**: {{What it means and what the agent produces. One sentence.}}

## Constraints

- DO NOT {{OUT_OF_SCOPE_ACTION_1}} — that is `{{OTHER_AGENT_NAME}}`'s domain.
- DO NOT {{OUT_OF_SCOPE_ACTION_2}} — that is `{{OTHER_AGENT_NAME}}`'s domain.
- DO NOT {{OUT_OF_SCOPE_ACTION_3}} — that is `{{OTHER_AGENT_NAME}}`'s domain.
- Read and search files for analysis; only write or replace the designated output files listed below.
- {{ANY_ADDITIONAL_HARD_CONSTRAINT_SPECIFIC_TO_THIS_AGENT.}}

## Evidence Rules

- Every material finding must cite at least one concrete file path.
- Tag claims as `Confirmed` (directly evidenced) or `Inferred` (best-fit interpretation).
- If evidence is missing, state `Not found in scanned files` — never guess.
- Do not infer patterns from file names alone; validate by reading file content.

## Approach

Follow the **{{N}}-step procedure** defined in `.github/skills/{{AGENT_NAME}}/SKILL.md`:

1. **{{Step 1 Name}}** — {{One-line summary of what this step produces or decides.}}
2. **{{Step 2 Name}}** — {{One-line summary.}}
3. **{{Step 3 Name}}** — {{One-line summary.}}
4. **{{Step 4 Name}}** — {{One-line summary.}}
5. **{{Step 5 Name}}** — {{One-line summary.}}
6. **{{Step 6 Name}}** — {{One-line summary.}}

## Output File

Create folder `{{OUTPUT_FOLDER}}/` and write both artifacts (always overwrite, never append):

| File | Contents |
|------|----------|
| `{{OUTPUT_FOLDER}}/{project_name}-{{ARTIFACT_SLUG}}.md` | {{Description of what this markdown file contains — sections, structure, purpose.}} |
| `{{OUTPUT_FOLDER}}/{project_name}-{{ARTIFACT_SLUG}}.html` | {{Description of what this HTML file contains — diagrams, visuals, interactivity.}} |

- If a required file does not exist, create it and write the full content.
- If a required file already exists, replace the entire file content in one operation — always overwrite, never append.
- **Writing both output files is mandatory. The analysis is not complete until both files are created.**
- Do NOT return artifact content in chat as a substitute for writing the files to disk.

## Output Format

The output format for both files is fully defined in `.github/skills/{{AGENT_NAME}}/SKILL.md` under the **Output Format** section:

- **`{project_name}-{{ARTIFACT_SLUG}}.md`** — Sections: {{Section A}} · {{Section B}} · {{Section C}} · {{Section D}} · {{Section E}}.
- **`{project_name}-{{ARTIFACT_SLUG}}.html`** — {{Description of the HTML output: diagram types, theme, interactivity requirements.}}

Always replace ALL placeholder labels in the STANDARDS.md template with actual content found during analysis.
