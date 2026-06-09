# 🔍 Prompt 01 — Measure Inventory

## Objective

Generate a complete inventory of every DAX measure in the semantic model.

## Instructions

> **Copilot Agent Mode prompt — paste into the chat panel:**

```
@workspace Scan all files under /source/ — specifically reportExtensions.json
and any .tmdl files under /definition/tables/ — and produce a comprehensive
inventory of every DAX measure in this Power BI model.

For each measure output:
- Measure name
- DAX expression (full text)
- Format string (if defined)
- Display folder (if defined)
- Source file path
- Any dependencies on other measures (cross-references)

Output as a Markdown table to /audit/reports/audit_findings.md under a
"## Measure Inventory" heading. Also output a CSV version to
/audit/baseline/measures_inventory.csv.
```

## Expected Output

- `audit/reports/audit_findings.md` — Markdown inventory table
- `audit/baseline/measures_inventory.csv` — CSV export

## Post-step

Commit: `git commit -m "audit: 01 — measure inventory generated"`
