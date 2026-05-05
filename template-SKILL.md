---
name: {AGENT_NAME}
description: '{{SKILL_DESCRIPTION_USED_FOR_SKILL_SELECTION_MAX_120_CHARS}}'
argument-hint: '{{WHAT_THE_CALLER_ARGUMENT_REPRESENTS_EG_PROJECT_NAME_OR_PATH}}'
---

# {{Skill Display Name}}

# Instructions

1. **Before executing**, read [SKILL.md](./SKILL.md) for the step-by-step procedure and [STANDARDS.md](./STANDARDS.md) for exact output templates, syntax rules, and validation checklists.
2. Execute all steps in the **Procedure** section below in order. Do not skip or reorder steps.
3. After writing each output file, read it back to confirm it was written correctly and matches the expected structure from STANDARDS.md.
4. **Run validation** against the checklist in [STANDARDS.md](./STANDARDS.md) before declaring any step complete.
5. **Report validation results**:
   - If valid: confirm and proceed to the next step.
   - If invalid: list every failing check and explain what is wrong.
6. **Fix all issues automatically** — invalid output has no value and must not be left in place.
7. **Re-validate** to confirm every fix resolved its issue.
8. Repeat steps 6–7 until all validation checks pass.

## Role
**{{Job Title}}** — {{One or two sentences defining the skill's mission and primary deliverable. Specify what the skill produces, not just what it does.}}

## Output Location
Create folder `{{OUTPUT_FOLDER}}/` and produce:
- `{project_name}-{{ARTIFACT_SLUG}}.md` — {{Description of the markdown artifact: what sections it contains, who will read it.}}
- `{project_name}-{{ARTIFACT_SLUG}}.html` — {{Description of the HTML/visual artifact: diagrams, interactivity, rendering requirements.}}

> **Always overwrite these files completely — never append.** Appending produces duplicate document structures that break rendering and invalidate the output.

---

## Procedure

### Step 1 — {{Step Name: Discovery / Identification}}
{{Detailed instructions for what to find and how. Include what to look for, what files or patterns to scan, and what constitutes a complete result for this step.}}

Key questions to answer in this step:
- {{Question 1 that drives the analysis — make it specific.}}
- {{Question 2 that drives the analysis.}}
- {{Question 3 that drives the analysis.}}

Produce a working list of {{ITEMS_FOUND}} before moving to Step 2.

### Step 2 — {{Step Name: Boundary / Inventory Mapping}}
{{Detailed instructions for step 2. Map or catalogue what was found in Step 1.}}

For each item found in Step 1:
- Record its **name**, **location** (file path), and **primary responsibility**.
- Mark it as `{{PROPERTY_A}}`, `{{PROPERTY_B}}`, or `{{PROPERTY_C}}`.
- Identify any **shared kernel** — components consumed by multiple items.
- Identify **cross-cutting concerns**: {{examples relevant to this skill's domain}}.

Output a table with columns: `{{Column 1}}` | `{{Column 2}}` | `{{Column 3}}` | `{{Column 4}}`.

### Step 3 — {{Step Name: Pattern / Relationship Analysis}}
{{Detailed instructions for step 3. How do the mapped items interact or relate?}}

Map {{RELATIONSHIP_TYPE}} by category:

| Category | Description | Items Involved | Coupling Severity |
|---|---|---|---|
| {{Category 1}} | {{What this pattern means}} | {{Which items}} | High / Medium / Low |
| {{Category 2}} | {{What this pattern means}} | {{Which items}} | High / Medium / Low |

### Step 4 — Generate Output Files
Follow [STANDARDS.md](./STANDARDS.md) for all templates, format rules, and syntax constraints.

Use the base template from STANDARDS.md as the starting document and populate every section with content from Steps 1–3.

**Required sections** (match the structure defined in STANDARDS.md):
- **4.1** — {{Section name and one-line purpose.}}
- **4.2** — {{Section name and one-line purpose.}}
- **4.3** — {{Section name and one-line purpose.}}
- **4.4** — {{Section name and one-line purpose.}}
- **4.5** — {{Section name and one-line purpose.}} *(skip if {{CONDITION_THAT_MAKES_IT_IRRELEVANT}})*
- **4.6** — {{Section name and one-line purpose.}}

> **Important**: Replace ALL placeholder labels in the STANDARDS.md template with actual content discovered during analysis. The template is a starting point only — every node, label, and entry must reflect the real system.

### Step 4.1 — Validate Generated Output
After writing the output files, run through the **File Creation Validation Checklist** in [STANDARDS.md](./STANDARDS.md) before proceeding.

Key checks specific to this skill's output:
- {{Check 1 specific to this skill — e.g., "All {{N}} required sections are present."}}
- {{Check 2 specific to this skill — e.g., "No placeholder `{{PLACEHOLDER}}` strings remain."}}
- {{Check 3 specific to this skill — e.g., "Every table has at least one data row."}}
- {{Check 4 specific to this skill.}}

If any check fails, fix the file using the safest approach (targeted edits or full regeneration), then rerun the complete checklist. The step is complete only when all checks pass.

### Step 5 — Identify Weaknesses / Issues
Document at least **{{MIN_FINDING_COUNT}}** findings. More is better; fewer is a gap.

| # | Finding | Evidence (file:line) | Impact | Remediation Effort |
|---|---|---|---|---|
| 1 | {{Finding name — concise noun phrase}} | `{{path/to/file.ext:line}}` | High / Medium / Low | High / Medium / Low |
| 2 | {{Finding name}} | `{{path/to/file.ext:line}}` | High / Medium / Low | High / Medium / Low |
| 3 | {{Finding name}} | `{{path/to/file.ext:line}}` | High / Medium / Low | High / Medium / Low |

Tag each finding as `Confirmed` or `Inferred` per [core-standards.md](../../standards/core-standards.md).

### Step 6 — {{Final Step Name: Synthesis / Summary}}
{{Detailed instructions for the final step. What synthesis or summary must the agent produce? What are the key hotspots, constraints, or recommendations that result from the full analysis?}}

Identify the top **{{N}}** items with the highest combined Impact + Remediation Effort score. These are the priority findings.

---

## Output Format

Output templates, syntax rules, and the File Creation Validation Checklist are defined in [STANDARDS.md](./STANDARDS.md). STANDARDS.md is the single authoritative source for output structure — do not duplicate templates here.

---

## Definition of Done (DoD)

### Completeness
- [ ] `{project_name}-{{ARTIFACT_SLUG}}.md` written to `{{OUTPUT_FOLDER}}/` and confirmed readable
- [ ] `{project_name}-{{ARTIFACT_SLUG}}.html` written to `{{OUTPUT_FOLDER}}/` and confirmed readable
- [ ] All {{N}} required sections present in each output file
- [ ] No `{{PLACEHOLDER}}` strings remaining in any output file
- [ ] At least {{MIN_FINDING_COUNT}} findings documented in Step 5 with evidence citations

### Technical Accuracy
- [ ] {{Accuracy check 1 — e.g., "All integrations mapped with their protocol (HTTP, gRPC, DB direct, etc.)"}}
- [ ] {{Accuracy check 2 — e.g., "Sync vs. async flows clearly distinguished."}}
- [ ] {{Accuracy check 3 — e.g., "All shared data stores identified with their full consumer list."}}
- [ ] Every material claim tagged `Confirmed` or `Inferred`
- [ ] Every `Confirmed` claim cites a file path

### Validation
- [ ] All items in the STANDARDS.md File Creation Validation Checklist passed
- [ ] Output files read back after writing and confirmed correct
- [ ] {{Skill-specific validation step — e.g., "HTML renders without errors in a browser."}}
- [ ] No failing validation check left unresolved

---
