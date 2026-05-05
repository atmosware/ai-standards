# {{Skill Display Name}} Standards

> **Tier 2 — Skill-local standards.** Extends [Core Standards (Tier 1)](../../standards/core-standards.md).
> Core standards apply universally; this file adds `{{AGENT_NAME}}`-specific output templates, syntax rules, and validation checklists.

Reference templates for producing `{project_name}-{{ARTIFACT_SLUG}}.html` and `{project_name}-{{ARTIFACT_SLUG}}.md`.
Replace ALL placeholder labels with actual content from analysis — templates are starting points only.

> **CRITICAL FILE RULE**: Always **overwrite** output files completely — **NEVER append**.
> If a file already exists, replace its entire contents in one write operation. Appending produces duplicate document structures that break rendering.

---

## Output Template
> if your output file needs a fixed format or structure you should define here. for example for html and mermaidjs you can use related formats.


---

## Syntax Rules & Common Errors

If there are rules for your agent you should define here as:

### Rule 1 
...

### Rule 2
...

---

## File Creation Validation Checklist

After generating each output file, verify every item before marking the step complete:

1. **File exists** — confirm the write succeeded at the exact expected path (`{{OUTPUT_FOLDER}}/{project_name}-{{ARTIFACT_SLUG}}.ext`)
2. **Single document** — the document opener (e.g., `<!DOCTYPE html>` or `# Title`) appears exactly **once** in the file
3. **Required sections present** — all {{N}} required sections exist in the file with correct headings
4. **No placeholder text** — no `{{PLACEHOLDER}}` strings remain anywhere in the output
5. **No empty sections** — every section contains substantive content, not just a heading
6. **No empty tables** — every table has at least one data row
7. **Evidence cited** — every `Confirmed` claim cites a file path; every `Inferred` claim states its basis
8. **Ratings consistent** — all severity/effort ratings use exactly `High`, `Medium`, or `Low`
9. **{{SKILL_SPECIFIC_CHECK_1}}** — {{What to verify and how.}}
10. **{{SKILL_SPECIFIC_CHECK_2}}** — {{What to verify and how.}}
11. **{{SKILL_SPECIFIC_CHECK_3}}** — {{What to verify and how.}}

If any check fails, **overwrite the entire file** with corrected content — never patch individual lines.

---

## Output Document Structure

### {project_name}-{{ARTIFACT_SLUG}}.md

```markdown
# {{System Name}} — {{Report Title}}

## 1. {{Section 1 Name}}
[{{Description of what this section contains — one sentence.}}]

## 2. {{Section 2 Name}}
### 2.1 {{Subsection Name}}
| {{Col A}} | {{Col B}} | {{Col C}} | {{Col D}} |
|---|---|---|---|
| {{value}} | {{value}} | {{value}} | {{value}} |

### 2.2 {{Subsection Name}}
[{{Description.}}]

## 3. {{Section 3 Name}}
### 3.1 {{Subsection Name}}
### 3.2 {{Subsection Name}}
### 3.3 {{Subsection Name}}

## 4. {{Section 4 Name}}
[{{Description.}}]

## 5. {{Section 5 Name}}
| # | Finding | Evidence (file:line) | Impact | Remediation Effort |
|---|---|---|---|---|
| 1 | {{Finding}} | `{{path:line}}` | High / Medium / Low | High / Medium / Low |

## 6. {{Section 6 Name}}
[{{Description.}}]

## 7. {{Section 7 Name}}
[{{Constraints, recommendations, and handoff notes.}}]
```

---

## Finding Table Template

Use this table structure for all finding inventories. Minimum {{MIN_FINDING_COUNT}} rows required.

| # | Finding | Evidence (file:line) | Impact | Remediation Effort |
|---|---|---|---|---|
| 1 | {{Finding — concise noun phrase}} | `{{path/to/file.ext:line}}` | High | High |
| 2 | {{Finding — concise noun phrase}} | `{{path/to/file.ext:line}}` | Medium | Medium |
| 3 | {{Finding — concise noun phrase}} | `{{path/to/file.ext:line}}` | Low | Low |

Use `High / Medium / Low` for all Impact and Remediation Effort values.
Tag each row `Confirmed` or `Inferred` in a **Tag** column when the distinction is material.
