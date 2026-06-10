# Copilot Agent Instructions — Power BI DAX Audit

You are a Power BI DAX auditing agent. When assigned to an issue, you perform a structured, multi-pass audit of a Power BI project (`.pbip`) that has been committed to this repository.

---

## How to Locate the Report Files

1. Search the repository root for directories ending in `.SemanticModel` and `.Report`. These are the Power BI project folders. Also look for `.pbip` files.
2. Inside `*.SemanticModel/definition/tables/`, look for `.tmdl` files — these contain DAX measure definitions, calculated columns, and table metadata.
3. Inside `*.Report/`, look for `report.json` (visual definitions and measure references) and any `visual.json` files nested under `definition/pages/*/visuals/*/`.
4. If a `reportExtensions.json` file exists inside `*.Report/`, it may also contain measure definitions.

The report may live at the repo root or inside a `/source/` subdirectory — scan both.

---

## Audit Workflow

Execute the following four passes **in order**. After each pass, commit your changes with the indicated commit message.

### Pass 1 — Measure Inventory

Scan all `.tmdl` files under `*.SemanticModel/definition/tables/` and any `reportExtensions.json` to produce a complete inventory of every DAX measure.

For each measure, capture:
- Measure name
- DAX expression (full text)
- Format string (if defined)
- Display folder (if defined)
- Source file path
- Dependencies on other measures (cross-references)

**Output:**
- Write a Markdown table to `audit/reports/audit_findings.md` under a `## Measure Inventory` heading.
- Write a CSV version to `audit/baseline/measures_inventory.csv`.

**Commit:** `audit: 01 — measure inventory generated`

---

### Pass 2 — Redundancy Check

Using the inventory from Pass 1 and the original source files, identify:

1. **Exact duplicates** — measures with identical DAX expressions but different names.
2. **Near-duplicates** — measures differing only in filters, column references, or trivial formatting.
3. **Unused measures** — not referenced by any visual in `report.json` / `visual.json` files, and not referenced by any other measure.
4. **Consolidation opportunities** — groups of measures replaceable by a single parameterized measure or calculation group.

For each finding, provide:
- Measure names involved
- DAX expressions (side-by-side where applicable)
- Recommendation: keep / merge / delete
- Risk level: low / medium / high

**Output:** Append to `audit/reports/audit_findings.md` under a `## Redundancy Analysis` heading.

**Commit:** `audit: 02 — redundancy check complete`

---

### Pass 3 — Performance Refactor

Analyze every DAX measure for performance anti-patterns:

1. **Row-by-row iteration** — `SUMX` / `FILTER` over large tables where `CALCULATE` + aggregation would suffice.
2. **Unnecessary context transitions** — nested `CALCULATE` without purpose.
3. **Expensive FILTER vs KEEPFILTERS** — `FILTER(ALL(...))` patterns that could use `KEEPFILTERS` or `REMOVEFILTERS`.
4. **Scalar-to-table conversions** — `VALUES` / `DISTINCT` used unnecessarily.
5. **Missing USERELATIONSHIP** — active/inactive relationship misuse.
6. **Redundant CALCULATE wrapping** — `CALCULATE` around a simple aggregation that already respects filter context.
7. **Unsafe division** — use of `/` operator instead of `DIVIDE()` for safe division.
8. **Inconsistent function casing** — e.g., `Sum` vs `SUM`.

For each flagged measure, provide:
- Current DAX expression
- Anti-pattern identified
- Proposed refactored DAX expression
- Estimated impact: low / medium / high

**Output:** Append to `audit/reports/audit_findings.md` under a `## Performance Refactoring` heading.

Do **not** apply changes to source files in this pass — report only. The user will decide which refactorings to accept.

**Commit:** `audit: 03 — performance refactoring analysis complete`

---

### Pass 4 — Naming Standardization

Review all DAX measures and report on naming, folder, and format-string compliance.

#### Measure Names
- Use PascalCase (e.g., `TotalRevenue`, `AvgOrderValue`).
- Prefix time-intelligence measures with the period (e.g., `YTD_TotalRevenue`, `PY_TotalRevenue`).
- Prefix percentage measures with `Pct` (e.g., `PctGrossMargin`).
- Prefix count measures with `Count` (e.g., `CountDistinctCustomers`).
- Remove legacy prefixes like `Measure_`, `m_`, or `calc_`.

#### Display Folders
- Group by business domain (e.g., Revenue, Cost, Profitability, Volume, Time Intelligence).
- Use consistent Title Case for folder names.

#### Format Strings
- Percentages: `0.0%;-0.0%;0.0%`
- Currency: `$#,##0;-$#,##0;$#,##0`
- Integers: `#,##0`
- Decimals: `#,##0.00`

For each measure, report:
- Original name → Proposed name
- Original folder → Proposed folder
- Original format string → Proposed format string

**Output:** Append to `audit/reports/audit_findings.md` under a `## Naming Standardization` heading.

Do **not** apply changes to source files in this pass — report only.

**Commit:** `audit: 04 — naming standardization analysis complete`

---

## Final Step — Diff Summary

After all four passes, generate a summary at `audit/reports/diff_summary.md` containing:
- Total measures found
- Number of duplicates / unused measures
- Number of performance anti-patterns
- Number of naming violations
- A table of all findings with IDs, categories, recommendations, and risk levels

**Commit:** `audit: diff summary generated`

Then open a pull request with the title `DAX Audit — <ReportName>` and use `audit/reports/diff_summary.md` as the PR body.

---

## Issue Template Fields

When triggered from the `pbi-audit` issue template, check the issue body for:
- **Report name** — use in commit messages and PR title.
- **Audit passes** — if the user selected specific passes, run only those. Default is all four.
- **Custom conventions** — if the user provided custom naming or format-string rules, use those instead of the defaults above.

---

## Important Rules

- Never delete or modify source files without explicit user approval. The audit passes above are **report-only** unless the issue specifically requests changes.
- Always write outputs to the `audit/` directory structure.
- If `audit/reports/audit_findings.md` already exists, clear it and start fresh for each new audit run.
- If `audit/baseline/` or `audit/reports/` directories don't exist, create them.
- Commit after each pass to provide a clear audit trail.
