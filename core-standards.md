# Core Standards

> **Tier 1 — Universal.** Every agent and skill in this system inherits these standards without exception.
> Skill-local standards (Tier 2) may add specificity but must never contradict this document.

---

## 1. Evidence Rules

Every material finding, claim, or assertion must follow these rules:

| Tag | Meaning | When to use |
|---|---|---|
| `Confirmed` | Directly evidenced by file content, config, log, or code path you have read | Cite the exact file path |
| `Inferred` | Best-fit interpretation based on indirect or circumstantial evidence | Label explicitly; include the basis for the inference |
| `Not found` | Evidence is absent from scanned files | Use this phrase verbatim — never guess in its place |

- Every material claim must cite at least one concrete file path, line number, or artifact.
- Do not infer patterns from file names alone; validate by reading file content.
- If two interpretations are equally plausible, present both and label the more likely one `Inferred`.

---

## 2. File Operation Rules

- **Always overwrite output files completely** — never append to an existing file.
- If the file already exists, replace its entire contents in a single write operation.
- After writing, confirm the write succeeded at the exact expected path before proceeding.
- Do not return artifact content in chat as a substitute for writing the file to disk.
- Log the output path explicitly when the write is complete.

---

## 3. Scope Enforcement

- Each agent operates within a defined domain. Read the **Constraints** section of the agent definition before starting work.
- If a finding belongs to another agent's domain, flag it in a `Handoff Note` and stop. Do not produce the other agent's deliverable.
- Read and search files freely. Only write to the output paths designated in your agent definition.
- When in doubt whether a finding is in scope, it is not — surface it as a handoff.

---

## 4. Output Conventions

- Use **tables** for structured comparisons and inventories.
- Use **numbered lists** for ordered procedures where sequence matters.
- Use **bullet lists** for unordered sets of items.
- Rate severity and effort as `High / Medium / Low` consistently across all agents.
- When referencing code, include the file path and line number where known: `path/to/file.ext:42`.
- Tag each material claim with `Confirmed` or `Inferred` wherever accuracy is material to the reader.

---

## 5. Uncertainty Handling

- Prefer `Not found in scanned files` over any form of guessing.
- Never fabricate file paths, function names, class names, configuration values, or version numbers.
- If a required piece of evidence is missing, state the gap explicitly and continue with the remaining steps.
- Uncertainty about scope → consult the agent Constraints section before proceeding.

---

## 6. Step Compliance

- **Do NOT skip, reorder, or summarise steps** defined in a SKILL.md.
- All validation checklists are mandatory — do not abbreviate, batch, or defer them.
- If a required step cannot be completed, state the blocker explicitly, document what was completed, and stop cleanly.
- Validation failures must be fixed before the step is marked complete; partial completion is not completion.

---

## 7. Agent Handoff Protocol

When your analysis surfaces a finding that falls outside your scope:

1. Write a `## Handoff Note` section at the end of your output.
2. Name the target agent explicitly (e.g., `cognia-po`, `cognia-ux`).
3. Summarise the finding in one sentence.
4. Stop. Do not invoke the other agent, chain it, or produce its deliverable.

Example:

```markdown
## Handoff Note
**Target agent**: `{{PREFIX}}-po`
**Finding**: The checkout module contains three user-facing copy strings that contradict the product brief — these require product owner review before the next release.
```

---

## 8. Security & Safety Rules

- Do not write credentials, secrets, API keys, or PII to any output file.
- If a scanned file contains credentials or PII, note their presence but do not reproduce the values.
- Do not execute, compile, or deploy code as part of analysis — read only.
- Do not follow symlinks outside the designated project root during file scanning.
