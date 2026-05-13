# {{Skill Display Name}} Standards

> **Tier 2 — Skill-local standards.** Extends [Core Standards (Tier 1)](../../standards/core.md).
> Core standards apply universally; this file adds `{{AGENT_NAME}}`-specific output templates, syntax rules, and validation checklists.

Reference templates for producing `{project_name}-{{ARTIFACT_SLUG}}.html` and `{project_name}-{{ARTIFACT_SLUG}}.md`.
Replace ALL placeholder labels with actual content from analysis — templates are starting points only.

> **CRITICAL FILE RULE**: Always **overwrite** output files completely — **NEVER append**.
> If a file already exists, replace its entire contents in one write operation. Appending produces duplicate document structures that break rendering.

---

## Output Template

### `{project_name}-{{ARTIFACT_SLUG}}.html`

Use this scaffold for every HTML output file. Replace all `{{PLACEHOLDER}}` values with real content.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>{{REPORT_TITLE}} — {project_name}</title>
  <script src="https://cdn.jsdelivr.net/npm/mermaid/dist/mermaid.min.js"></script>
  <style>
    *, *::before, *::after { box-sizing: border-box; }
    body { font-family: system-ui, sans-serif; margin: 0; background: #0d1117; color: #c9d1d9; line-height: 1.6; }
    nav { position: sticky; top: 0; background: #161b22; border-bottom: 1px solid #30363d; padding: 0.75rem 1.5rem; display: flex; gap: 1.5rem; flex-wrap: wrap; z-index: 100; }
    nav a { color: #58a6ff; text-decoration: none; font-size: 0.875rem; }
    nav a:hover { text-decoration: underline; }
    main { max-width: 1100px; margin: 0 auto; padding: 2rem 1.5rem; }
    h1 { font-size: 1.75rem; border-bottom: 1px solid #30363d; padding-bottom: 0.5rem; }
    h2 { font-size: 1.25rem; margin-top: 2.5rem; border-left: 3px solid #58a6ff; padding-left: 0.75rem; }
    h3 { font-size: 1rem; color: #8b949e; }
    table { width: 100%; border-collapse: collapse; margin: 1rem 0; font-size: 0.875rem; }
    th { background: #161b22; color: #8b949e; text-align: left; padding: 0.5rem 0.75rem; border: 1px solid #30363d; }
    td { padding: 0.5rem 0.75rem; border: 1px solid #30363d; vertical-align: top; }
    tr:nth-child(even) { background: #161b22; }
    .badge { display: inline-block; padding: 0.15rem 0.5rem; border-radius: 4px; font-size: 0.75rem; font-weight: 600; }
    .high   { background: #3d1c1c; color: #f85149; }
    .medium { background: #2d2008; color: #e3b341; }
    .low    { background: #0d2216; color: #3fb950; }
    pre.mermaid { background: #161b22; border: 1px solid #30363d; border-radius: 6px; padding: 1rem; overflow-x: auto; }
    details summary { cursor: pointer; font-weight: 600; padding: 0.5rem 0; color: #58a6ff; }
    details[open] summary { margin-bottom: 0.5rem; }
    /* Accessibility */
    :focus-visible { outline: 2px solid #58a6ff; outline-offset: 2px; }
    @media (prefers-reduced-motion: reduce) { * { transition: none !important; } }
  </style>
</head>
<body>
  <nav aria-label="Report sections">
    <a href="#section-1">{{Section 1}}</a>
    <a href="#section-2">{{Section 2}}</a>
    <a href="#section-3">{{Section 3}}</a>
    <a href="#findings">Findings</a>
    <a href="#handoffs">Handoff Notes</a>
  </nav>

  <main>
    <h1>{{REPORT_TITLE}}</h1>
    <p><strong>Project:</strong> {project_name} &nbsp;|&nbsp; <strong>Generated:</strong> {{DATE}}</p>

    <section id="section-1">
      <h2>{{Section 1 Name}}</h2>
      <p>{{Content}}</p>
    </section>

    <section id="section-2">
      <h2>{{Section 2 Name}}</h2>
      <table>
        <thead><tr><th>{{Col A}}</th><th>{{Col B}}</th><th>{{Col C}}</th></tr></thead>
        <tbody>
          <tr><td>{{value}}</td><td>{{value}}</td><td>{{value}}</td></tr>
        </tbody>
      </table>
    </section>

    <section id="section-3">
      <h2>{{Section 3 Name}} — Diagram</h2>
      <pre class="mermaid">
graph TD
  A[{{Node A}}] --> B[{{Node B}}]
      </pre>
    </section>

    <section id="findings">
      <h2>Risk Matrix</h2>
      <table>
        <thead><tr><th>#</th><th>Finding</th><th>Evidence</th><th>Impact</th><th>Effort</th></tr></thead>
        <tbody>
          <tr>
            <td>1</td>
            <td>{{Finding}}</td>
            <td><code>{{path/to/file.ext:line}}</code></td>
            <td><span class="badge high">High</span></td>
            <td><span class="badge high">High</span></td>
          </tr>
        </tbody>
      </table>
    </section>

    <section id="handoffs">
      <h2>Handoff Notes</h2>
      <p>{{None. | Table of out-of-scope findings for other agents.}}</p>
    </section>
  </main>

  <script>mermaid.initialize({ startOnLoad: true, theme: 'dark' });</script>
</body>
</html>
```

**Rules for HTML output:**
- `<!DOCTYPE html>` must appear exactly once.
- All Mermaid diagrams must use `<pre class="mermaid">` blocks — never `<div>` or `<script>` tags.
- No inline `style=""` attributes on content elements; use the stylesheet classes above.
- Every `<section>` must have a matching `<a href>` in `<nav>`.
- Severity badges must use exactly the CSS classes `high`, `medium`, or `low`.
- `lang` attribute on `<html>` is required for accessibility.

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

If any check fails, correct the file using targeted edits or full regeneration, then rerun all checklist items. The file is valid only when every check passes.

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
