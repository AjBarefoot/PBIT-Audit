# 🔁 Prompt 02 — Redundancy Check

## Objective

Identify duplicate, overlapping, or redundant measures that can be consolidated.

## Instructions

> **Copilot Agent Mode prompt:**

```
@workspace Using the measure inventory from /audit/reports/audit_findings.md
and the source files under /source/, identify:

1. **Exact duplicates** — measures with identical DAX expressions but different names.
2. **Near-duplicates** — measures with expressions that differ only in filters,
   column references, or trivial formatting.
3. **Unused measures** — measures not referenced by any visual in
   report.json or by any other measure.
4. **Consolidation opportunities** — groups of measures that could be replaced
   by a single parameterized measure or calculation group.

For each finding, provide:
- Measure names involved
- DAX expressions (side-by-side where applicable)
- Recommendation (keep / merge / delete)
- Risk level (low / medium / high)

Append results to /audit/reports/audit_findings.md under a
"## Redundancy Analysis" heading.
```

## Expected Output

- Updated `audit/reports/audit_findings.md` with redundancy findings

## Post-step

Commit: `git commit -m "audit: 02 — redundancy check complete"`
