# ⚡ Prompt 03 — Performance Refactor

## Objective

Identify and refactor DAX measures with known performance anti-patterns.

## Instructions

> **Copilot Agent Mode prompt:**

```
@workspace Analyze every DAX measure in the /source/ files for performance
anti-patterns. Flag any measure that uses:

1. **Row-by-row iteration** — SUMX / FILTER over large tables where
   CALCULATE + aggregation would suffice.
2. **Unnecessary context transitions** — nested CALCULATE without purpose.
3. **Expensive FILTER vs KEEPFILTERS** — FILTER(ALL(...)) patterns that
   could use KEEPFILTERS or REMOVEFILTERS.
4. **Scalar-to-table conversions** — VALUES / DISTINCT used unnecessarily.
5. **Missing USERELATIONSHIP** — active/inactive relationship misuse.
6. **Redundant CALCULATE wrapping** — CALCULATE around a simple aggregation
   that already respects filter context.

For each flagged measure:
- Current DAX expression
- Anti-pattern identified
- Proposed refactored DAX expression
- Estimated impact (low / medium / high)

Output to /audit/reports/audit_findings.md under a
"## Performance Refactoring" heading.

If confident in the refactoring, also apply the changes directly to the
source files (reportExtensions.json and/or .tmdl files) and note which
files were modified.
```

## Expected Output

- Updated `audit/reports/audit_findings.md` with performance findings
- Optionally modified source files with refactored DAX

## Post-step

Commit: `git commit -m "audit: 03 — performance refactoring applied"`
