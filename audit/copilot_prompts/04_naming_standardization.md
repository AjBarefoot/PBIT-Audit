# 🏷️ Prompt 04 — Naming Standardization

## Objective

Enforce consistent naming conventions across all measures, display folders, and format strings.

## Instructions

> **Copilot Agent Mode prompt:**

```
@workspace Review all DAX measures in the /source/ files and standardize
naming using these conventions:

### Measure Names
- Use PascalCase (e.g., TotalRevenue, AvgOrderValue).
- Prefix time-intelligence measures with the period
  (e.g., YTD_TotalRevenue, MTD_GrossProfit, PY_TotalRevenue).
- Prefix percentage measures with "Pct" (e.g., PctGrossMargin).
- Prefix count measures with "Count" (e.g., CountDistinctCustomers).
- Remove prefixes like "Measure_", "m_", or "calc_".

### Display Folders
- Group by business domain: Revenue, Cost, Profitability, Volume, Time Intelligence.
- Use consistent casing for folder names.

### Format Strings
- Percentages: "0.0%;-0.0%;0.0%"
- Currency: "$#,##0;-$#,##0;$#,##0"
- Integers: "#,##0"
- Decimals: "#,##0.00"

For each change:
- Original name → New name
- Original folder → New folder
- Original format string → New format string

Apply all changes to the source files and output a summary to
/audit/reports/audit_findings.md under a
"## Naming Standardization" heading.
```

## Expected Output

- Updated source files with standardized names/folders/formats
- Updated `audit/reports/audit_findings.md` with change log

## Post-step

Commit: `git commit -m "audit: 04 — naming standardization applied"`
